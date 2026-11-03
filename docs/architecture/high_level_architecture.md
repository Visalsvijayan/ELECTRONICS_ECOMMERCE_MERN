# MERN Commerce — High-Level System Architecture

## Document Control

| Field | Details |
|---|---|
| Document ID | AR-001 |
| Document Version | 0.1 |
| Document Status | Approved |
| Project | MERN Commerce |
| Date | 02 November 2026 |
| Governing PRD | MC-PRD-001 v1.0 |
| Approval Authority | Product Owner |

## 1. Purpose

This document defines the high-level technical architecture of MERN Commerce. It establishes the major application components, their responsibilities, communication methods, and architectural principles.

## 2. Architecture Style

**Modular Monolith**

MERN Commerce will use a modular monolithic architecture. The frontend and backend will be independently organized applications, while the backend business domains will operate as logical modules within a single backend application.

This approach provides clear separation of responsibilities without introducing unnecessary microservice infrastructure and operational complexity.

## 3. Technology Stack

| Layer | Technology |
|---|---|
| Frontend | React + TypeScript |
| Backend | Node.js + Express + TypeScript |
| Database | MongoDB |
| API Style | REST |
| Data Format | JSON |
| Authentication | JWT-based authentication |
| Authorization | Role-Based Access Control (RBAC) |

## 4. Frontend Architecture

One React application will provide two experiences:

- Customer Storefront
- Administrator Dashboard

Both experiences will use shared frontend infrastructure while maintaining separate layouts, routes, and access permissions.

## 5. Backend Architecture

The backend will be a modular Express application containing:

1. Authentication and Users
2. Product Catalog
3. Cart and Pricing
4. Checkout and Orders
5. Inventory Management
6. Shipping and Tax
7. Cancellation and Returns
8. Administration

Each module will have clearly defined responsibilities and controlled interactions with other modules.

## 6. Database Architecture

MongoDB will serve as the primary persistence layer.

It will store customer and administrator information, products, variants, carts, orders, inventory records, shipping and tax configuration, return and cancellation records, COD/refund records, and audit history.

Detailed collection structures and indexes are defined separately in the database design documentation.

## 7. External Dependencies

The application may integrate with:

- Object/image storage for product images and return evidence.
- Notification services for transactional communications.

Specific providers will be selected during detailed design.

## 8. Communication Architecture

- Frontend-to-backend communication: HTTPS.
- API communication style: REST.
- Request and response format: JSON.
- Backend-to-database communication: MongoDB driver/ODM.

## 9. Security Principles

- JWT-based authentication.
- Backend-enforced RBAC.
- Server-side validation of untrusted input.
- Customer data isolation.
- Protected administrative operations.
- Secure handling of credentials and environment variables.

## 10. Critical Architectural Principles

1. The backend is the authoritative source for product prices, stock, shipping, tax, and order validation.
2. Checkout must prevent overselling through concurrency-safe inventory operations.
3. Historical orders must preserve price, address, and tax snapshots.
4. Order fulfillment and COD payment reconciliation must be tracked independently.
5. Cancellation, returns, and refunds must follow distinct business workflows.
6. Important administrative and financial actions must be auditable.

## 11. Architecture Approval

High-Level Architecture AR-001 v0.1 was formally approved by the Product Owner on 02 November 2026, subject to the approved PRD MC-PRD-001 v1.0.

Comments: None.

Detailed system design and implementation require separate authorization.