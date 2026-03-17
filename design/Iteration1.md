# Iteration 1 — Structural Decomposition of the System

---

## Step 2 — Iteration Goal and Selected Drivers

### Goal

> **Structurally decompose the system.** Choose the top-level architectural style, identify the major containers, and establish the cross-cutting concerns (offline operation, role-based access control, multi-branch data isolation) that will govern all subsequent design decisions.

This is a **greenfield** development, so the element to be refined in this first iteration is the **whole system**.

### Drivers selected for this iteration

#### Constraints

| ID | Description |
|---|---|
| RES-01 | System must operate offline and sync automatically on reconnection (3 of 5 branches have intermittent connectivity). |
| RES-02 | Must support up to 40 concurrent users distributed across 5 branches. |
| RES-03 | Interface must be fully functional on PCs, tablets and smartphones (responsive). |
| RES-06 | Must implement RBAC for 6 distinct roles. |
| RES-07 | Offline sync must include a reliable conflict-resolution strategy. |
| RES-08 | Must handle 700–1,100 orders/day at franchise level. |
| RES-09 | Must run on existing hardware (5 PCs, 10–14 tablets, 5 TVs, personal smartphones). |

#### Quality attribute scenarios

| ID | Attribute | Scenario summary |
|---|---|---|
| QA-AVA-01 | Availability | ≥ 99.5% monthly uptime across all 5 branches during operating hours. |
| QA-AVA-02 | Availability | Cloud server failure → branches continue offline; service restored in ≤ 15 min. |
| QA-REL-01 | Reliability | Branch offline 2 h, records 40 orders → 100% synced, 0 losses on reconnection. |
| QA-REL-03 | Reliability | 3 branches re-connect at different times → 100% consistent global state, no duplicates. |

#### Architectural concerns

| ID | Description |
|---|---|
| C001.2.1 | Offline-online sync strategy — guarantee consistency with intermittent and multi-device offline operation. |
| C001.2.2 | Local data persistence — define where and how data is stored locally on each device/branch. |
| C002.1.1 | Inter-module integration — cohesive modules with low coupling. |
| C003.1.1 | RBAC implementation — robust authentication and authorization for all six roles. |
| C004.3.1 | Continuity when cloud hub fails — branches keep running critical functions. |
| C005.1.1 | Module boundary definition — enable parallel development without regressions. |
| C007.1.1 | Multi-branch data structure — support 5 branches + concurrent users + order volume without degradation. |
| C007.1.2 | Isolation vs. shared data — define what is shared across branches and what is branch-local. |
| C008.1.1 | Critical process identification — determine which processes cannot be interrupted. |

---

## Step 3 — Elements of the System to Refine

Since this is a **greenfield** development and **iteration 1**, there are no previously designed elements. The single element to refine is the **whole system**, approached via **top-down decomposition**.

| Element to refine | Refinement type | Rationale |
|---|---|---|
| **The whole system** | Top-down decomposition | No prior architecture exists. The domain model defines *what* the system manages but not *how* capabilities are deployed. This iteration produces the first layer of containers that serve as the baseline for all subsequent iterations. |

---

## Step 4 — Design Concepts That Satisfy the Selected Drivers

| Design Concept | Type | Pros | Cons | Discarded Alternatives |
|---|---|---|---|---|
| **Modular Monolith + Cloud Sync Hub** | Reference Architecture | Local-first satisfies RES-01 & QA-AVA-02. Runs on existing hardware (RES-09). Low operational overhead. Hub enables consolidated reporting. Module boundaries support modifiability. | Sync conflict resolution non-trivial (RES-07). Single process per branch — poor module isolation if boundaries not enforced. | Pure Cloud SaaS *(breaks under intermittent connectivity)*; Microservices *(operational overhead unsustainable)*; Central DB Client-Server *(single point of failure)*; Event Sourcing *(overkill)*; Peer-to-Peer *(no authority node)* |
| **Offline-First / Local-First pattern** | Architectural Pattern | Branch fully operational without internet. Writes locally first, syncs later. Directly satisfies RES-01, QA-AVA-02, QA-REL-01/03. | Requires sync queue and conflict resolution (detailed in Iteration 3). All writes must carry timestamp + device ID. | Online-first with cache *(insufficient)*; No offline support *(eliminates 3 of 5 branches)* |
| **Outbox Pattern + Sync Queue** | Architectural Pattern | Guarantees no data loss on dropped connectivity (QA-REL-01). Idempotent replay prevents duplicates (QA-REL-03). Decouples write from sync. | Two writes per operation (entity + outbox entry). Requires background sync worker on each branch node. | Fire-and-forget HTTP sync *(loses messages)*; Polling without queue *(misses events)* |
| **Role-Based Access Control (RBAC)** | Architectural Pattern | Enforces least-privilege across 6 roles (RES-06). Auditable. Satisfies QA-SEC-01/02/03. | Permission matrix must be maintained as roles evolve. Session management on shared devices adds complexity (C003.1.3). | ABAC *(too complex for team size)*; Hardcoded per-screen checks *(not maintainable)* |
| **Intra-module layering** | Architectural Pattern | Each module structured as **Public API/Facade → Application → Domain → Infrastructure**. The Public API is the only allowed entry point — the Presentation layer and other modules call it exclusively through this interface, never through internal layers or cross-schema DB queries. Enforces cohesion (C002.1.1, C005.1.1). | Risk of layer violations without tooling enforcement. | Single horizontal layered stack *(couples modules)*; Big Ball of Mud *(eliminates modifiability)*; Hexagonal/Ports & Adapters *(more complex than needed at this stage)* |
| **Multi-Page Web Application (MPA, server-rendered)** | External Component | Simpler than SPA for MVP: no client build toolchain, no client router, no state manager. Offline met inherently (server is local on branch LAN). Single codebase for PCs, tablets, smartphones (RES-03). | Full page reloads on navigation (acceptable for operational POS at this volume). Real-time views may need SSE in future. | SPA *(unnecessary complexity for MVP)*; Native apps *(multiply maintenance cost)* |
| **Local relational DB per branch node** | External Component | ACID transactions protect financial integrity (QA-REL-02). PostgreSQL schemas enforce module data isolation. Viable on existing PCs (RES-09). | Schema migrations must be managed consistently across branches. | In-memory store *(data lost on crash)*; Document NoSQL *(weaker ACID for financial data)* |

> **Deferred to Iteration 3:** The specific connectivity-detection mechanism (e.g., heartbeat) and the conflict-resolution algorithm (e.g., Last-Write-Wins with entity versioning) are acknowledged as necessary by the Offline-First and Outbox patterns above, but their design will be refined when HU-27, QA-AVA-02, QA-REL-01/03 and RES-07 are addressed in detail.

---

## Step 5 — Instantiate Architectural Elements

| Instantiation Decision | Rationale |
|---|---|
| Create one **Branch Node** per branch (5 total) — a self-contained deployable unit running on the existing branch PC | Instantiates Modular Monolith + Offline-First. Each branch operates autonomously from the cloud. Satisfies RES-01, RES-09, QA-AVA-02, C004.3.1. |
| The Branch Node hosts a **Branch Application Server** — a modular monolith with modules: *Identity & Access*, *Order Management*, *Product Catalog*, *Inventory*, *Financial Operations* | Each module organized as **Public API/Facade → Application → Domain → Infrastructure**. Single shared Presentation Layer at application level calls modules only through their Public API. Modules call each other only through Public APIs — never through internal layers or cross-schema DB queries. Satisfies C002.1.1, C005.1.1. |
| The Branch Node includes a **Local PostgreSQL DB** — each module owns a dedicated schema (`identity`, `orders`, `catalog`, `inventory`, `financial`) plus a shared `sync` schema for the SyncQueue outbox | PostgreSQL schemas enforce module data isolation at DB level without separate DB instances. ACID guarantees protect financial integrity (QA-REL-02). SyncQueue enables loss-free sync (QA-REL-01). Satisfies C001.2.2, C005.1.1. |
| The Branch Node includes a **Sync Worker** — a background OS-level process (daemon) collocated on the same branch PC | Reads `PENDING` entries from `sync.sync_queue` and pushes to Cloud Sync Hub when internet is available. Marks entries `SYNCED`, `CONFLICT`, or `FAILED`. Not a separate machine — no extra hardware required. Satisfies QA-REL-01, QA-REL-03, C001.2.1. |
| The Branch Node serves a **Responsive Web Frontend** — a server-rendered MPA accessible via browser on PCs and tablets, structured into role-gated sections: *POS View*, *Kitchen Display View*, *Manager View* | Server-side rendering is sufficient — "offline" means no internet, not no local server. No native app install required. Satisfies RES-03, RES-09, RES-06. |
| An **Auth Module** within the Branch Node — handles login, session management, RBAC enforcement, caches role/permission table locally | Local cache enables authentication without cloud connectivity. Satisfies C003.1.1, C003.1.3, C003.1.4, RES-06. |
| Create one **Cloud Sync Hub** — cloud-hosted, with a **Sync API** (REST write) and a **Central PostgreSQL DB** | Receives sync payloads from all Branch Sync Workers, applies to Central DB, returns conflict markers. Authority node for cross-branch consistency. Satisfies C007.1.1, C007.1.2, QA-REL-03. |
| The Cloud Sync Hub exposes a **Reporting API** — separate read-only REST endpoint | Serves aggregated multi-branch data exclusively to the owner. Separates sync write traffic from reporting read traffic. To be detailed in Iteration 5. Satisfies C007.1.1. |

> **Not instantiated in this iteration:** The QR digital menu (RES-05, HU-22/23) and the Kitchen TV display (RES-04, HU-07) will be instantiated in Iterations 5 and 6 respectively.

---

## Step 6 — Views, Responsibilities and Design Decisions

### Container Diagram (C4 Level 2)

> See `LaToscana_ContainerDiagram.puml` in the `design/` folder.


#### Container responsibilities

| Container | Who accesses it | Responsibility |
|---|---|---|
| **MPA Web Frontend** | Staff browsers — local LAN only | Server-rendered HTML. Role-gated sections: POS View, Kitchen Display View, Manager View. In-process to App Server. |
| **Branch Application Server** | MPA Web Frontend (in-process) | Modular monolith with all branch business logic. Each module accessed only through its Public API/Facade. |
| **Local PostgreSQL DB** | App Server (SQL); Sync Worker (sync schema) | Branch-local data persistence. One schema per module + shared `sync` schema for outbox. ACID guarantees. |
| **Sync Worker** | Local DB (reads); Cloud Sync Hub (writes) | Background daemon on branch PC. Drains SyncQueue, pushes to hub, marks results. |
| **Sync API** | Sync Workers from all 5 branches | REST write endpoint. Receives sync payloads, applies to Central DB, returns conflict markers. |
| **Reporting API** | Owner browser — internet only | Read-only REST. Serves consolidated multi-branch data exclusively to owner. |
| **Central PostgreSQL DB** | Sync API (writes); Reporting API (reads) | Consolidated data from all branches. Source of truth for cross-branch reporting. |

---

### Component Diagram (C4 Level 3 — Branch Application Server)

> See `LaToscana_ComponentDiagram_BranchServer.puml` in the `design/` folder.


#### Component responsibilities

| Component | Responsibility |
|---|---|
| **Presentation Layer** | Handles all HTTP requests. Session/auth checks via Identity Public API. Delegates to module Public APIs. Renders response. Single shared layer for all modules. |
| **Identity & Access Module** | Users, roles, permissions, sessions. RBAC enforcement. Locally cached permission table for offline auth. |
| **Order Management Module** | Creates/tracks orders and order lines. Table status management. Status changes (SENT_TO_KITCHEN, READY). Writes sync events to outbox. |
| **Product Catalog Module** | Products, categories, recipes. Read-heavy. Shared by Order Management for product lookup. |
| **Inventory Module** | Ingredient stock per branch. Low-stock alerts. Waste/loss adjustments. Writes stock events to outbox. |
| **Financial Operations Module** | Sales, payments, receipts, cash-register cuts. Reads closed orders from Order Management. Writes financial events to outbox. |

### Design decisions

| Driver | Decision | Rationale | Discarded Alternatives |
|---|---|---|---|
| RES-01, RES-09, QA-AVA-02, C004.3.1 | One self-contained **Branch Node** per branch on existing branch PC | Branches must operate offline. Local node eliminates internet dependency. No extra hardware. | Pure Cloud SaaS; Thin client to central server |
| RES-01, QA-REL-01, QA-REL-03, C001.2.1 | **Offline-First + Outbox Pattern** — writes to local DB first; Sync Worker replays to hub on reconnection | Zero data loss during offline periods. Idempotent replay prevents duplicates. Decouples write performance from network. | Fire-and-forget HTTP sync; Polling without queue |
| RES-06, QA-SEC-01/02/03, C003.1.1, C003.1.4 | **RBAC with locally cached permission table** in Auth Module | Roles enforced even without internet. Local cache enables offline authentication. | ABAC (too complex); Online-only RBAC (fails offline) |
| RES-03, RES-09 | **Server-rendered MPA** instead of SPA | Server always reachable on branch LAN. No client build toolchain or state manager needed for MVP. Migrating to SPA later is feasible — only the Presentation Layer changes. | SPA (unnecessary for MVP); Native apps (multiply maintenance) |
| C001.2.2, C005.1.1 | **One PostgreSQL schema per module** within single Local DB | DB-level isolation without separate DB instances. Modules communicate through Application-layer APIs, not cross-schema joins. | Separate DB per module (overhead); Shared schema (no isolation); Document NoSQL (weak ACID) |
| C002.1.1, C005.1.1 | **Public API/Facade** as only external entry point per module | Module boundaries explicit and enforceable. Prevents coupling via internal classes or DB queries. Enables independent testing and future migration. | Direct cross-module calls; Shared service layer |
| C007.1.1, C007.1.2 | **Cloud Sync Hub** with separate Sync API (write) and Reporting API (read) | Separates sync and reporting traffic. Hub is authority node for cross-branch aggregation. Kept thin in Iteration 1. | Branch-to-branch sync (no authority node); Reporting embedded in branch (no consolidated view) |

---

## Step 7 — Analysis of Current Design

| Driver | Result | Justification |
|---|---|---|
| RES-01 — Offline operation | 🟡 Partially satisfied | Local-first topology and Outbox + Sync Worker establish the structural foundation. Conflict-resolution algorithm and connectivity-detection deferred to Iteration 3. |
| RES-02 — 40 concurrent users | 🟡 Partially satisfied | Load distributed across 5 independent Branch Nodes (~8–12 users each). No performance/capacity analysis yet. |
| RES-03 — Responsive PCs/tablets/smartphones | 🟢 Satisfied | MPA Web Frontend establishes a single server-rendered codebase for all browser-capable devices on the branch LAN. |
| RES-06 — RBAC for 6 roles | 🟡 Partially satisfied | Auth Module with locally-cached RBAC identified structurally. Detailed permission matrix defined in Iteration 3. |
| RES-07 — Conflict-resolution strategy | 🟡 Partially satisfied | SyncQueue establishes the detection mechanism. Specific resolution algorithm deferred to Iteration 3. |
| RES-08 — 700–1,100 orders/day | 🟡 Partially satisfied | Distributed topology (~140–220 orders/branch/day) is structurally manageable. No load testing defined yet. |
| RES-09 — Existing hardware | 🟢 Satisfied | Branch Node on existing branch PC. MPA requires no client-side installation. |
| QA-AVA-01 — ≥ 99.5% uptime | 🟡 Partially satisfied | Local-first addresses branch-level uptime. Cloud hub availability addressed in Iterations 3 and 5. |
| QA-AVA-02 — Cloud fails, branches continue | 🟢 Satisfied | Branch Node fully self-contained. Sync Worker suspends gracefully. No branch function depends on cloud. |
| QA-REL-01 — 0% data loss after offline | 🟡 Partially satisfied | Outbox Pattern guarantees local write persistence. Idempotent replay and conflict resolution deferred to Iteration 3. |
| QA-REL-03 — Consistent global state post-sync | 🟡 Partially satisfied | Cloud Sync Hub as single authority node establishes correct topology. Merge/conflict protocol deferred to Iteration 3. |
| C001.2.1 — Offline-online sync strategy | 🟡 Partially satisfied | Strategy established (Outbox → Sync Worker → Cloud Hub). Ordering, deduplication, and conflict details in Iteration 3. |
| C001.2.2 — Local data persistence | 🟢 Satisfied | Local PostgreSQL with one schema per module fully defined at architectural level. |
| C002.1.1 — Inter-module integration, low coupling | 🟢 Satisfied | Public API/Facade pattern is the only allowed inter-module channel. Cross-schema queries forbidden. |
| C003.1.1 — RBAC implementation | 🟡 Partially satisfied | Auth Module structurally defined. Permission granularity, session policy, and offline token strategy in Iteration 3. |
| C004.3.1 — Continuity when cloud hub fails | 🟢 Satisfied | Branch Nodes operate independently. All critical branch functions are entirely local. |
| C005.1.1 — Module boundary definition | 🟢 Satisfied | Five modules named, schemas assigned, Public API/Facade pattern and no-cross-schema rule enforce boundaries. |
| C007.1.1 — Multi-branch data structure | 🟢 Satisfied | 5 Branch Nodes + Central DB at Cloud Sync Hub establishes coherent multi-branch topology. |
| C007.1.2 — Isolation vs. shared data | 🟢 Satisfied | Branch-local in Local DB (isolated per branch). Cross-branch consolidated in Central DB. Schemas isolate modules within each branch. |
| C008.1.1 — Critical process identification | 🟡 Partially satisfied | Branch Node autonomy implicitly identifies branch operations as critical. Formal categorization table is a deployment concern for Iteration 3. |

### Iteration goal review

> **Goal:** *Structurally decompose the system — choose the top-level architectural style, identify major containers, and establish cross-cutting concerns.*

**Substantially achieved.** 8 of 20 drivers are fully **Satisfied**; 12 are **Partially satisfied** — in every case intentionally, with the remaining design decisions explicitly deferred to the iteration whose drivers directly address them. No driver is **Not satisfied**.

The architecture has a solid, justified skeleton that all subsequent iterations will build upon.
