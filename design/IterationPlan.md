# Iteration Plan — La Toscana Franchise Management System

## Overview

This plan organizes the ADD design process into six iterations. Driver prioritization follows the criteria established in `ArchitecturalDrivers.md`: (1) direct impact on economic loss reduction ($33,000–$58,000 MXN/month), (2) alignment with business needs (NEC-01 to NEC-09), (3) technical dependencies between modules, and (4) quality attribute difficulty/importance.

---

## Iteration Plan Table

| # | Goal | Drivers Addressed |
|---|------|-------------------|
| **1** | **Structurally decompose the system.** Define the overall architecture by choosing the top-level architectural style (modular monolith on a local server + cloud sync hub), identifying the major containers, and establishing cross-cutting concerns such as offline operation and role-based access control. This gives the whole system an initial shape on which subsequent iterations will build. | **Constraints:** RES-01, RES-02, RES-03, RES-04, RES-05, RES-06, RES-07, RES-08, RES-09 · **QA:** QA-AVA-01, QA-AVA-02, QA-REL-01, QA-REL-03 · **Concerns:** C001.2.1, C001.2.2, C002.1.1, C003.1.1, C004.3.1, C005.1.1, C007.1.1, C007.1.2, C008.1.1 |
| **2** | **Support the core point-of-sale flow (orders and payments).** Design the Order Management and Financial Operations modules so that waiters can register orders with full traceability and cashiers can calculate totals and close sales. This directly eliminates the unregistered/modified orders and manual calculation errors that generate the highest share of monthly losses. | **HU:** HU-01, HU-02, HU-04, HU-05, HU-06 · **QA:** QA-PERF-01, QA-PERF-02, QA-USA-01, QA-USA-03, QA-SEC-02 · **Concerns:** C002.1.2, C002.1.3, C002.2.1, C002.2.2, C002.3.1, C002.3.2, C003.3.1 |
| **3** | **Implement role-based security and offline operation.** Harden the authentication and authorization subsystem (RBAC for all six roles) and make the system fully functional when internet connectivity is unavailable. These are mandatory pre-conditions for production rollout in the three branches with intermittent connectivity. | **HU:** HU-27, HU-28 · **QA:** QA-SEC-01, QA-SEC-02, QA-SEC-03, QA-AVA-02, QA-REL-01, QA-REL-02, QA-REL-03 · **Constraints:** RES-01, RES-06, RES-07 · **Concerns:** C001.2.1, C001.2.2, C001.2.3, C003.1.1, C003.1.2, C003.1.3, C003.1.4, C003.2.1, C003.2.2, C004.3.1 |
| **4** | **Enable inventory control and automated cash-register cut.** Design the Inventory module (real-time stock, low-stock alerts, waste/loss registration) and the automated cash-register closing. These directly address the second and third largest loss sources: inventory waste (10–15 % of input costs) and the 32 man-hours per branch per month spent on manual closing. | **HU:** HU-10, HU-11, HU-12, HU-13, HU-14 · **QA:** QA-PERF-02, QA-REL-02, QA-MOD-01 · **Concerns:** C001.1.1, C001.1.2, C001.3.1, C001.3.2, C002.1.2, C003.3.1, C003.3.2, C007.1.3 |
| **5** | **Provide consolidated reporting, centralized catalog, kitchen display, and purchasing.** Give the owner and managers the visibility tools (multi-branch dashboard, report export, product catalog administration, supplier and purchase-order management) and complete the kitchen/waiter notification loop. These features have medium business priority: they depend on the transaction data produced in previous iterations and have no alternative manual workaround left. | **HU:** HU-03, HU-07, HU-08, HU-09, HU-15, HU-16, HU-17, HU-18, HU-19, HU-20 · **QA:** QA-PERF-03, QA-USA-02, QA-AVA-03, QA-MOD-01, QA-MOD-02 · **Constraints:** RES-03, RES-04 · **Concerns:** C001.4.1, C001.4.2, C002.2.1, C004.1.1, C004.1.2, C004.1.3, C004.2.1, C004.2.2, C004.2.3, C005.2.1, C005.2.2, C006.1.1, C006.1.2, C006.1.3, C006.2.1, C006.2.2, C007.2.1, C007.2.2 |
| **6** | **Add value-added and future-growth features.** Design the QR digital menu for diners, recipe management with automatic ingredient deduction, promotions engine, customer registry, and loyalty groundwork. These features are low-priority (🟠 Baja) because they do not directly reduce the current losses, but they support future revenue growth and customer experience. | **HU:** HU-21, HU-22, HU-23, HU-24, HU-25, HU-26 · **QA:** QA-USA-02, QA-MOD-03 · **Constraints:** RES-05 · **Concerns:** C001.1.3, C001.3.3, C003.2.2, C005.1.2, C005.1.3, C005.3.1, C005.3.2, C006.3.1, C008.2.1, C008.2.2, C009.1.1, C009.1.2, C009.1.3, C009.2.1, C010.1.1, C010.1.2, C010.1.3, C010.1.4, C010.2.1, C010.2.2 |

---

## Rationale for Ordering

```
Iteration 1 → System skeleton (architecture style, containers, cross-cutting decisions)
    ↓
Iteration 2 → Core revenue flow: orders + payments (highest loss impact)
    ↓
Iteration 3 → Security + offline (mandatory for production at all 5 branches)
    ↓
Iteration 4 → Inventory + cash-cut (second-highest loss impact)
    ↓
Iteration 5 → Reporting + catalog + kitchen + purchasing (medium priority, data-dependent)
    ↓
Iteration 6 → Value-added: QR menu, promotions, loyalty (low priority, future growth)
```

Each iteration builds on the data and modules produced by the previous one, progressively reducing the $33,000–$58,000 MXN/month loss from the most impactful changes first.
