# MERN Commerce — Detailed System Design

## Document Control

| Field | Details |
|---|---|
| Document ID | DD-001 |
| Document Version | 0.1 |
| Document Status | In Progress |
| Project | MERN Commerce |
| Date | 02 November 2026 |
| Governing PRD | MC-PRD-001 v1.0 |
| Governing Architecture | AR-001 v0.1 |

## 1. Purpose

This document defines the detailed technical design of MERN Commerce, including frontend architecture, backend architecture, database design, API contracts, security, business workflows, and testing strategy.

The design must remain consistent with the approved product requirements and high-level architecture.

## 2. Frontend Application Architecture

### 2.1 Architecture Approach

The frontend will use React and TypeScript with a feature-based organization.

One frontend application will provide:

- Customer Storefront.
- Administrator Dashboard.

### 2.2 Proposed Folder Structure

- public/
- src/assets/
- src/components/
- src/features/
- src/layouts/
- src/pages/
- src/routes/
- src/services/
- src/hooks/
- src/contexts/
- src/store/
- src/types/
- src/utils/
- src/constants/
- src/styles/

### 2.3 Feature Organization

Business features will be organized independently under `features/`.

Examples:

- auth/
- products/
- categories/
- cart/
- checkout/
- orders/
- inventory/
- cancellations/
- returns/
- admin/

Each feature may contain its own components, hooks, services, types, and utilities.

### 2.4 State Management

Redux Toolkit will be used where shared or complex application state requires centralized management.

Simple component-level state will remain local to the relevant components.

Redux will not be introduced unnecessarily.

## 3. Backend Application Architecture

### 3.1 Architecture Approach

The backend will use Express and TypeScript with a modular layered architecture.

Business domains will remain logical modules within one backend application.

### 3.2 Proposed Folder Structure

- src/config/
- src/modules/
- src/middlewares/
- src/routes/
- src/database/
- src/utils/
- src/types/
- src/validators/
- src/errors/
- src/app.ts
- src/server.ts

### 3.3 Internal Module Structure

Each business module will follow a consistent structure where appropriate.

Example: Products module

- product.routes.ts
- product.controller.ts
- product.service.ts
- product.repository.ts
- product.model.ts
- product.validation.ts
- product.types.ts

### 3.4 Layer Responsibilities

| Layer | Responsibility |
|---|---|
| Routes | Defines API endpoints |
| Middleware | Authentication, authorization and request processing |
| Validation | Validates incoming data |
| Controller | Handles HTTP requests and responses |
| Service | Implements business logic |
| Repository | Handles database access |
| Model | Defines database document structure |

Not every module must contain unnecessary layers or files. The structure should remain consistent without adding complexity without purpose.

## 4. Design Approval Record

Section 2 — Frontend and Backend Application Structure:

Approved by the Product Owner on 02 November 2026.

Approved decisions:

- Feature-based React frontend organization.
- Separate customer and admin experiences.
- Redux Toolkit where shared or complex state requires it.
- Express modular layered backend architecture.
- Separation of routes, middleware, validation, controllers, services, repositories, and models.

## 5. Remaining Design Sections

| Section | Status |
|---|---|
| Application and module architecture | Proposed; pending review |
| Frontend and backend structure | Approved |
| MongoDB database design | Pending |
| REST API specification | Pending |
| Authentication and security design | Pending |
| Order and inventory workflows | Pending |
| Validation and error handling | Pending |
| Testing strategy | Pending |

## 6. Implementation Authorization

This document is a work in progress.

Approval of individual sections does not constitute approval of the complete detailed system design.

Application code generation and implementation require separate authorization.