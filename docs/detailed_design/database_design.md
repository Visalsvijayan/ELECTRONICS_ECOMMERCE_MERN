# MERN Commerce — Database Design Document

## Document Control

| Field | Details |
|---|---|
| Document ID | DB-001 |
| Version | 0.1 |
| Status | Draft — Under Review |
| Project | MERN Commerce |
| Database | MongoDB |
| ODM | Mongoose (Proposed) |
| Governing PRD | MC-PRD-001 v1.0 |
| Governing Architecture | AR-001 v0.1 |

## 1. Purpose
Define the logical and physical database design for MERN Commerce.

## 2. Database Design Principles
- Business-oriented data modelling.
- Appropriate embedding and referencing.
- Data consistency and concurrency safety.
- Historical order snapshots.
- Unique constraints and indexes.
- Auditable financial and inventory operations.
Inventory Data Model



Inventory Reservation Data Model
Reservation Lifecycle and State Transitions
Stock Movement Ledger
Inventory Indexing Strategy
Transaction and Concurrency Requirements

## 3. Proposed Collections
1. users
2. categories
3. products
4. productVariants
5. carts
6. inventory
7. stockMovements
8. serviceablePinCodes
9. shippingConfigs
10. taxConfigs
11. orders
12. codTransactions
13. cancellationRequests
14. returnRequests
15. refunds
16. auditLogs

## 4. Entity Relationships
[Insert the approved logical relationship diagram.]

## 5. Embedding and Referencing Strategy
[Document embedded and referenced relationships.]

## 6. Collection Data Dictionary
[Define fields, data types, required status, defaults and validation rules for every collection.]

## 7. Indexing Strategy
[Document indexes, uniqueness and query justification.]

## 8. Data Integrity and Consistency
[Document inventory, order, payment and refund consistency rules.]

## 9. Soft Deletion and Data Retention
[Document deactivation and retention rules.]

## 10. Database Approval Record
Pending Product Owner review and approval.



### Inventory Reservation Release Policy

**Decision:** Option B — immediate release on explicit checkout cancellation or automatic release at expiry, whichever occurs first.

**Reservation duration:** 15 minutes.

**Reservation start:** The reservation starts only after the backend successfully validates the customer's cart, current prices, inventory availability and delivery eligibility, and successfully reserves the required stock.

**Release conditions:**

1. When a customer explicitly cancels an active checkout attempt, the system must immediately release the associated reserved inventory.
2. If the customer does not complete checkout or cancel it, the reservation must be released automatically when its 15-minute expiry time is reached.
3. When a valid COD order is successfully created before expiry, the active reservation must be converted into a committed order allocation.

**Important rules:**

- Opening the checkout page alone must not reserve inventory.
- Explicit checkout cancellation is different from cancellation of an already-created order. Order cancellation follows the separate order cancellation workflow.
- A released, expired or committed reservation must never be processed again.
- Inventory release and reservation status updates must be performed atomically.
- The system must prevent duplicate inventory releases when customer cancellation and automatic expiry occur concurrently.
- Every inventory change must generate an immutable stock movement record.
- A committed reservation must not be released by the expiry process.
- Reservation expiry must be handled by a background expiry process, not by relying on MongoDB TTL deletion.

**Acceptance criteria:**

- Cancelling an active checkout releases its reserved stock immediately.
- An active reservation expires after 15 minutes if checkout is neither completed nor explicitly cancelled.
- A successful COD order commits the reservation.
- Concurrent cancellation and expiry processing cannot release the same reservation twice.
- A committed reservation cannot be expired or released by the reservation expiry process.
- Stock movement records accurately reflect every reservation and release operation.