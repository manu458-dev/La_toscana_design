### 1.- Introduction
<!-- Create a description of the document -->
### 2.- Context diagram
<!-- Include the context diagram from the
[FILE:ArchitecturalDrivers.md] document, if available. Include a paragraph at the beginning that describes what this diagram shows.
-->
### 3.- Architectural drivers
<!-- Include a summary of the drivers described in
[FILE:ArchitecturalDrivers.md], including their priorities. You
should separate user stories, quality attribute scenarios, concerns
and constraints in separate tables. -->
### 4.- Domain model

This domain model captures the core business concepts of the **La Toscana** franchise management system.
It is derived from the functional requirements (HU-01 to HU-28), the quality attribute scenarios and the architectural constraints defined in `ArchitecturalDrivers.md`.
The model is organized around seven bounded contexts: **Identity & Access**, **Order Management**, **Product Catalog**, **Inventory**, **Financial Operations**, **Purchasing**, and **Reporting**.

```plantuml
@startuml LaToscana_DomainModel
skinparam classAttributeIconSize 0
skinparam groupInheritance 2
hide empty members

' ── Identity & Access ─────────────────────────────────────────────────
package "Identity & Access" {

    class User {
        +String id
        +String name
        +String email
        +String passwordHash
        +login()
        +logout()
    }

    enum Role {
        OWNER
        MANAGER
        CASHIER
        WAITER
        BARISTA
        COOK
    }

    class Permission {
        +String id
        +String resource
        +String action
    }

    User "1" --> "1" Role : has
    Role "1" --> "*" Permission : grants
}

' ── Franchise & Branch ────────────────────────────────────────────────
package "Franchise & Branch" {

    class Franchise {
        +String id
        +String name
    }

    class Sucursal {
        +String id
        +String name
        +String location
        +Boolean onlineStatus
    }

    Franchise "1" --> "1..*" Sucursal : operates
}

User "*" --> "1" Sucursal : belongs to

' ── Product Catalog ───────────────────────────────────────────────────
package "Product Catalog" {

    class Product {
        +String id
        +String name
        +String description
        +Decimal price
        +String photoUrl
        +Boolean available
    }

    class Category {
        +String id
        +String name
    }

    class Recipe {
        +String id
        +String preparation
    }

    class RecipeLine {
        +Decimal quantity
        +String unit
    }

    class Ingredient {
        +String id
        +String name
        +String unit
    }

    Product "*" --> "1"  Category   : belongs to
    Product "1" --> "0..1" Recipe   : defined by
    Recipe  "1" *-- "*" RecipeLine  : composed of
    RecipeLine "*" --> "1" Ingredient : uses
}

' ── Order Management ──────────────────────────────────────────────────
package "Order Management" {

    class Order {
        +String id
        +DateTime createdAt
        +Decimal total
    }

    enum OrderStatus {
        OPEN
        SENT_TO_KITCHEN
        READY
        CLOSED
        CANCELLED
    }

    enum OrderType {
        DINE_IN
        TAKEAWAY
    }

    class OrderLine {
        +int quantity
        +Decimal unitPrice
        +String notes
    }

    class Table {
        +String id
        +int number
    }

    enum TableStatus {
        AVAILABLE
        OCCUPIED
    }

    Order "1"  --> "1"   OrderStatus : has
    Order "1"  --> "1"   OrderType   : is of
    Order "1"  *-- "*"   OrderLine   : contains
    Order "*"  --> "0..1" Table      : assigned to
    Table "1"  --> "1"   TableStatus : has
    OrderLine "*" --> "1" Product    : references
}

Order "*" --> "1" Sucursal : belongs to

' ── Financial Operations ──────────────────────────────────────────────
package "Financial Operations" {

    class Sale {
        +String id
        +DateTime closedAt
        +Decimal total
    }

    enum PaymentMethod {
        CASH
        CARD
    }

    class Receipt {
        +String id
        +DateTime issuedAt
        +String content
    }

    class CashRegisterCut {
        +String id
        +Date date
        +Decimal expectedAmount
        +Decimal actualAmount
        +Decimal difference
    }

    class Promotion {
        +String id
        +String name
        +String description
        +Decimal discount
        +DateTime startDate
        +DateTime endDate
        +Boolean active
    }

    Sale "1"  --> "1"    Order         : closes
    Sale "1"  --> "1"    PaymentMethod : paid by
    Sale "1"  --> "1"    Receipt       : generates
    Sale "*"  --> "0..1" Promotion     : applies
    CashRegisterCut "*" --> "*" Sale   : consolidates
}

CashRegisterCut "*" --> "1" Sucursal : for

' ── Inventory ─────────────────────────────────────────────────────────
package "Inventory" {

    class InventoryItem {
        +String id
        +Decimal stock
        +Decimal minLevel
    }

    class StockAdjustment {
        +String id
        +DateTime date
        +Decimal quantity
        +String justification
    }

    enum AdjustmentReason {
        WASTE
        THEFT
        CORRECTION
        PURCHASE_RECEIPT
    }

    class StockAlert {
        +String id
        +DateTime triggeredAt
        +Boolean acknowledged
    }

    InventoryItem "*"  --> "1"  Ingredient      : tracks
    InventoryItem "1"  *-- "*"  StockAdjustment : records
    StockAdjustment "1" --> "1" AdjustmentReason : classified as
    InventoryItem "1"  --> "*"  StockAlert      : generates
}

InventoryItem "*" --> "1" Sucursal : kept at

' ── Purchasing ────────────────────────────────────────────────────────
package "Purchasing" {

    class Supplier {
        +String id
        +String name
        +String contactInfo
    }

    class SupplierProduct {
        +Decimal price
        +String unit
    }

    class PurchaseOrder {
        +String id
        +DateTime issuedAt
        +String status
    }

    class PurchaseOrderLine {
        +Decimal quantityOrdered
        +Decimal quantityReceived
        +Decimal unitCost
    }

    Supplier  "1"  --> "*"  SupplierProduct    : offers
    SupplierProduct "*" --> "1" Ingredient      : corresponds to
    PurchaseOrder "1" *-- "*" PurchaseOrderLine : contains
    PurchaseOrderLine "*" --> "1" SupplierProduct : references
    PurchaseOrder "*" --> "1" Supplier           : placed with
}

PurchaseOrder "*" --> "1" Sucursal : delivered to

' ── Customer & Loyalty ────────────────────────────────────────────────
package "Customer & Loyalty" {

    class Customer {
        +String id
        +String name
        +String contact
    }
}

Sale "*" --> "0..1" Customer : associated with

' ── Cross-cutting: Offline Sync ───────────────────────────────────────
package "Offline Sync" {

    class SyncQueue {
        +String id
        +String entityType
        +String entityId
        +String payload
        +DateTime queuedAt
    }

    enum SyncStatus {
        PENDING
        SYNCED
        CONFLICT
        FAILED
    }

    SyncQueue "1" --> "1" SyncStatus : has
    SyncQueue "*" --> "1" Sucursal   : queued at
}

' ── Cross-cutting: Audit Log ──────────────────────────────────────────
package "Audit" {

    class AuditLog {
        +String id
        +DateTime timestamp
        +String entityType
        +String entityId
        +String action
    }

    AuditLog "*" --> "1" User : performed by
}

@enduml
```

#### Domain model element descriptions

| Element | Type | Description |
|---|---|---|
| **User** | Entity | Represents a system user (employee). Holds credentials and is bound to exactly one `Role` and one `Sucursal`. Supports HU-28, QA-SEC-01/02/03, RES-06. |
| **Role** | Enumeration | The six operational roles defined in RES-06: OWNER, MANAGER, CASHIER, WAITER, BARISTA, COOK. |
| **Permission** | Value Object | Defines a granular access rule (resource + action) assigned to a `Role` via RBAC (C003.1.1, C003.1.2). |
| **Franchise** | Entity | The top-level organizational unit, owning all branches of La Toscana. Supports the multi-tenant data model (C007.1.1). |
| **Sucursal** | Entity | One of the five physical branches. Tracks its own `onlineStatus` to support offline operation (HU-27, RES-01). |
| **Product** | Entity | An item available for sale. Centralizes pricing, descriptions and photos for consistency across branches (HU-18, NEC-05). |
| **Category** | Entity | Groups products for filtering in the POS and the QR digital menu (HU-22, HU-23). |
| **Recipe** | Entity | The standardized preparation procedure linked to a `Product` (HU-08, HU-21, NEC-06). |
| **RecipeLine** | Value Object | One ingredient + quantity entry within a `Recipe`. Enables automatic inventory deduction per sale. |
| **Ingredient** | Entity | A raw material tracked in inventory. Shared between `Recipe` and `InventoryItem` (NEC-01, NEC-06). |
| **Order** | Entity | A customer order linked to a table or marked as take-away. Lifecycle goes from OPEN to CLOSED (HU-01, HU-02, HU-04, HU-06). Contains full traceability. |
| **OrderStatus** | Enumeration | State machine for an order: OPEN → SENT_TO_KITCHEN → READY → CLOSED / CANCELLED. Drives kitchen display and waiter notifications (HU-07, HU-09). |
| **OrderType** | Enumeration | DINE_IN for table service, TAKEAWAY for direct sales. Covers HU-06. |
| **OrderLine** | Value Object | A single product-quantity entry within an `Order`, capturing the price at the moment of sale. |
| **Table** | Entity | Represents a physical table at a branch. Maintains AVAILABLE / OCCUPIED status to support the cashier view (HU-04). |
| **TableStatus** | Enumeration | AVAILABLE or OCCUPIED, reflecting each table's current state. |
| **Sale** | Entity | Represents a closed, paid transaction tied to an `Order`. Records the payment method and links to a `Receipt` (HU-05, NEC-03). |
| **PaymentMethod** | Enumeration | CASH or CARD payment options available at the POS (HU-05). |
| **Receipt** | Entity | The purchase proof generated at the moment of payment (HU-05, C002.3.2). |
| **CashRegisterCut** | Entity | The daily financial closing for one branch: expected vs. actual cash, automated by the system (HU-10, HU-11, NEC-03). |
| **Promotion** | Entity | A timed discount applicable to sales. Managed centrally by the owner and reflected in the QR menu (HU-24, HU-25). |
| **InventoryItem** | Entity | Tracks the current stock of one `Ingredient` at one branch. Triggers low-stock alerts (HU-12, HU-13, NEC-01). |
| **StockAdjustment** | Entity | Records a manual change to inventory stock (waste, correction, receipt), with justification for audit purposes (HU-14, C003.3.1). |
| **AdjustmentReason** | Enumeration | Classifies inventory adjustments: WASTE, THEFT, CORRECTION, PURCHASE_RECEIPT. |
| **StockAlert** | Entity | Auto-generated notification when an `InventoryItem` drops to or below its minimum level (HU-13, QA-MOD-03). |
| **Supplier** | Entity | A provider of ingredients, including contact data and historical pricing (HU-19, NEC-02). |
| **SupplierProduct** | Value Object | Associates a `Supplier` with an `Ingredient` at a specific price and unit (HU-19, HU-20). |
| **PurchaseOrder** | Entity | A formal order sent to a `Supplier`. On reception, automatically updates `InventoryItem` stock (HU-20, NEC-02). |
| **PurchaseOrderLine** | Value Object | One line (ingredient, quantity ordered, quantity received, unit cost) within a `PurchaseOrder`. |
| **Customer** | Entity | Stores basic contact data for a guest to support future loyalty programs (HU-26, NEC-09). |
| **SyncQueue** | Entity | Queues entity mutations generated while a branch is offline, to be replayed upon reconnection (HU-27, RES-01, RES-07, C001.2.1). |
| **SyncStatus** | Enumeration | Lifecycle of a queued item: PENDING → SYNCED / CONFLICT / FAILED. |
| **AuditLog** | Entity | Immutable record of every sensitive action (who, what, when) for security traceability (QA-SEC-02, C003.3.1, C003.3.2). |



### 5.- Container diagram

This diagram shows the top-level containers that compose the La Toscana system as established in Iteration 1. There are five autonomous **Branch Nodes** (one per branch), each running on the existing branch PC, and one central **Cloud Sync Hub** hosted in the cloud. Each Branch Node is fully self-contained and operational without internet access. The Cloud Sync Hub aggregates data from all branches and exposes a reporting interface exclusively to the owner.

```mermaid
graph TB
    staffBrowser["Staff Browser<br/>waiter / cashier / manager / barista / cook<br/>Branch LAN - PCs and tablets"]
    ownerBrowser["Owner Browser<br/>any device, internet"]

    subgraph branchNode["Branch Node x5 - one per branch, existing branch PC"]
        direction TB
        webFE["MPA Web Frontend<br/>server-rendered HTML, responsive"]
        appServer["Branch Application Server<br/>Modular Monolith"]
        localDB[("Local PostgreSQL DB<br/>schemas: identity, orders, catalog,<br/>inventory, financial, sync")]
        syncWorker["Sync Worker<br/>background process,<br/>collocated on same PC"]

        webFE -- in-process --> appServer
        appServer -- SQL --> localDB
        syncWorker -- reads SyncQueue --> localDB
    end

    subgraph cloudHub["Cloud Sync Hub - cloud-hosted"]
        direction TB
        syncAPI["Sync API<br/>REST - write"]
        reportingAPI["Reporting API<br/>REST - read-only"]
        centralDB[("Central PostgreSQL DB<br/>consolidated, all branches")]

        syncAPI -- SQL --> centralDB
        reportingAPI -- SQL --> centralDB
    end

    staffBrowser -- HTTP local LAN only --> webFE
    syncWorker -- HTTPS POST --> syncAPI
    ownerBrowser -- HTTPS GET --> reportingAPI
```

> **Actor separation:** Staff browsers (waiters, cashiers, managers, baristas, cooks) access **only** the Branch Node MPA via local LAN — no direct access to the Cloud Sync Hub. The owner browser accesses **only** the Reporting API on the Cloud Sync Hub over the internet. Customers/diners are out of scope for this iteration (QR menu is addressed in Iteration 6).

> **Sync Worker colocation:** The Sync Worker is a background OS-level process (daemon/service) running on the **same physical branch PC** as the Branch Application Server and PostgreSQL. It is not a separate machine. It has no HTTP interface; it only reads from the local DB and pushes to the Cloud Sync Hub.

#### Container responsibilities

| Container | Who accesses it | Responsibility |
|---|---|---|
| **MPA Web Frontend** | Staff browsers — local LAN only | Serves server-rendered HTML pages to staff browsers on branch PCs and tablets. Provides role-gated sections: POS View, Kitchen Display View, Manager View. Calls the Branch Application Server in-process. |
| **Branch Application Server** | MPA Web Frontend (in-process) | Hosts the modular monolith with all branch-local business logic (Identity & Access, Order Management, Product Catalog, Inventory, Financial Operations). Each module accessed only through its Public API/Facade. |
| **Local PostgreSQL DB** | Branch App Server (SQL); Sync Worker (reads sync schema) | Persists all branch-local data using one schema per bounded-context module plus a shared `sync` schema for the SyncQueue outbox. Provides ACID guarantees for financial data integrity. |
| **Sync Worker** | Local DB (reads); Cloud Sync Hub (writes) | Background process collocated on the branch PC. Reads `PENDING` entries from `sync.sync_queue` and pushes them to the Cloud Sync Hub when internet is available. Marks entries `SYNCED`, `CONFLICT`, or `FAILED`. |
| **Sync API** | Sync Workers from all 5 branches | REST write endpoint on the Cloud Sync Hub. Receives sync payloads, applies them to the Central DB, returns conflict markers. |
| **Reporting API** | Owner browser — internet only | Read-only REST endpoint on the Cloud Sync Hub. Serves consolidated multi-branch data (sales, inventory, financials) exclusively to the owner. |
| **Central PostgreSQL DB** | Sync API (writes); Reporting API (reads) | Consolidated database at hub level. Stores data synced from all five branches. Source of truth for cross-branch reporting. |

### 6.- Component diagrams

#### 6.1 — Branch Application Server

This diagram shows the internal components of the Branch Application Server. The shared **Presentation Layer** (HTTP routes and controllers) is the only entry point from the browser. It delegates to the five bounded-context modules exclusively through each module's **Public API/Facade**. Modules may call each other only through Public APIs. Each module owns its own PostgreSQL schema; cross-schema joins are forbidden.

```mermaid
graph TB
    pres["Presentation Layer\n(HTTP Routes / Controllers — application-wide)"]

    subgraph modules["Bounded-Context Modules"]
        direction TB
        identity["Identity & Access Module\nPublic API \u2192 Application \u2192 Domain \u2192 Infrastructure\nschema: identity"]
        orders["Order Management Module\nPublic API \u2192 Application \u2192 Domain \u2192 Infrastructure\nschema: orders"]
        catalog["Product Catalog Module\nPublic API \u2192 Application \u2192 Domain \u2192 Infrastructure\nschema: catalog"]
        inventory["Inventory Module\nPublic API \u2192 Application \u2192 Domain \u2192 Infrastructure\nschema: inventory"]
        financial["Financial Operations Module\nPublic API \u2192 Application \u2192 Domain \u2192 Infrastructure\nschema: financial"]
    end

    syncSchema[("sync schema\n(SyncQueue outbox)")]

    pres -- calls Public API --> identity
    pres -- calls Public API --> orders
    pres -- calls Public API --> catalog
    pres -- calls Public API --> inventory
    pres -- calls Public API --> financial

    orders -- calls Public API --> catalog
    orders -- calls Public API --> inventory
    financial -- calls Public API --> orders

    orders -- writes outbox --> syncSchema
    inventory -- writes outbox --> syncSchema
    financial -- writes outbox --> syncSchema
```

#### Component responsibilities

| Component | Responsibility |
|---|---|
| **Presentation Layer** | Handles all HTTP requests. Parses input, enforces session/auth checks via Identity & Access Module, delegates to the appropriate module's Public API, and renders the response. Single shared layer for all modules. |
| **Identity & Access Module** | Manages users, roles, permissions and sessions. Authenticates requests and enforces RBAC. Caches the role/permission table locally to support offline authentication. |
| **Order Management Module** | Creates, updates and tracks orders and order lines. Manages table status. Communicates order status changes (SENT_TO_KITCHEN, READY) to the kitchen display. Writes sync events to the `sync` schema outbox. |
| **Product Catalog Module** | Maintains the centralized product catalogue (products, categories, recipes). Read-heavy; shared by Order Management for product lookup during order creation. |
| **Inventory Module** | Tracks ingredient stock levels per branch. Generates low-stock alerts. Records waste/loss adjustments. Writes stock change events to the outbox for sync. |
| **Financial Operations Module** | Manages sales, payment methods, receipts and cash-register cuts. Reads closed orders from Order Management via Public API. Writes financial events to the outbox for sync. |
| **sync schema / SyncQueue** | Shared outbox table written by all modules. Read exclusively by the Sync Worker. Stores entity mutations with status: PENDING → SYNCED / CONFLICT / FAILED. |

### 7.- Sequence diagrams

#### 7.1 — Offline Write and Synchronization Flow

This diagram illustrates the cross-cutting offline-first pattern: a branch operation (e.g., order creation) is written locally first and stored in the SyncQueue outbox. When the Sync Worker detects internet connectivity, it pushes pending entries to the Cloud Sync Hub. This flow satisfies **C001.2.1** (offline-online sync strategy), **QA-REL-01** (0% data loss after offline period), and **QA-REL-03** (consistent global state after multi-branch reconnection).

```mermaid
sequenceDiagram
    participant Browser
    participant AppServer as Branch App Server
    participant LocalDB as Local PostgreSQL
    participant SyncWorker as Sync Worker
    participant CloudHub as Cloud Sync Hub

    Browser->>AppServer: POST /orders (create order)
    AppServer->>LocalDB: INSERT INTO orders.orders (...)
    AppServer->>LocalDB: INSERT INTO sync.sync_queue (entity_type='order', status='PENDING')
    AppServer-->>Browser: 201 Created

    Note over SyncWorker: Polls periodically, detects connectivity
    SyncWorker->>LocalDB: SELECT * FROM sync.sync_queue WHERE status = 'PENDING'
    LocalDB-->>SyncWorker: [pending entries]
    SyncWorker->>CloudHub: POST /sync (payload with entity data)
    CloudHub-->>SyncWorker: 200 OK (or 409 Conflict with conflict markers)

    alt No conflict
        SyncWorker->>LocalDB: UPDATE sync_queue SET status = 'SYNCED'
    else Conflict detected
        SyncWorker->>LocalDB: UPDATE sync_queue SET status = 'CONFLICT'
        Note over SyncWorker: Conflict resolution deferred to Iteration 3
    end
```

### 8.- Interfaces
<!-- This section will include details about contracts- -->

### 9.- Design decisions

The following design decisions were made during **Iteration 1** to address the selected drivers.

| Driver | Decision | Rationale | Discarded Alternatives |
|---|---|---|---|
| RES-01, RES-09, QA-AVA-02, C004.3.1 | Deploy one self-contained **Branch Node** per branch running on the existing branch PC | Branches must operate fully offline. A local node eliminates internet dependency for day-to-day operations and runs on existing hardware without additional investment. | Pure Cloud SaaS *(inoperable without internet)*; Thin client to central server *(single point of failure)* |
| RES-01, QA-REL-01, QA-REL-03, C001.2.1 | **Offline-First + Outbox Pattern (SyncQueue)** — writes go to the local DB first; a Sync Worker replays them to the hub when connectivity is restored | Guarantees zero data loss during offline periods. Idempotent replay prevents duplicates on reconnection. Decouples write performance from network availability. | Fire-and-forget HTTP sync *(loses data on timeout)*; Polling without queue *(misses events during offline windows)* |
| RES-06, QA-SEC-01/02/03, C003.1.1, C003.1.4 | **RBAC with locally cached permission table** in the Auth Module | Six operational roles must be enforced even when the branch has no internet. A locally cached role/permission table enables offline authentication without contacting the Cloud Hub. | ABAC *(over-complex for team size)*; Online-only RBAC *(fails offline)* |
| RES-03, RES-09 | **Server-rendered Multi-Page Application (MPA)** instead of SPA | The Branch Application Server is always reachable on the local LAN — "offline" means no internet, not no local server. An MPA requires no client-side build toolchain, router, or state manager, making it significantly simpler for MVP. | SPA *(unnecessary complexity — only warranted if the client must work without the local server too)*; Native apps *(multiply maintenance cost)* |
| C001.2.2, C005.1.1 | **One PostgreSQL schema per bounded-context module** (`identity`, `orders`, `catalog`, `inventory`, `financial`, `sync`) within the single branch Local DB | Enforces data isolation at the DB level within a single DB instance — no separate DB processes per module. Modules cannot join across schemas; they must communicate through Application-layer Public APIs. | Separate DB instance per module *(operational overhead)*; Shared schema with prefixed tables *(no enforced isolation)*; Document NoSQL *(weaker ACID guarantees for financial data)* |
| C002.1.1, C005.1.1, QA-MOD-01 | Each module exposes a **Public API/Facade** as its only external entry point; internal layers are private | Makes module boundaries explicit and enforceable. Prevents coupling between modules through internal classes or DB queries. Enables independent development and testing of each module. | Direct cross-module calls into Application/Domain layers *(creates tight coupling)*; Shared service layer across modules *(couples all modules)* |
| C007.1.1, C007.1.2 | **Cloud Sync Hub** with separate Sync API (write) and Reporting API (read) backed by a Central PostgreSQL DB | Separates sync traffic from reporting traffic. The hub is the authority node for cross-branch data aggregation. Keeping the hub thin in Iteration 1 minimizes cloud complexity while enabling future refinement. | Branch-to-branch sync *(no authority node, conflict resolution intractable)*; Embedding reporting in each branch *(no consolidated view for owner)* |

