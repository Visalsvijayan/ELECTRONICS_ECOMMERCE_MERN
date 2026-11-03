 # MERN Commerce — Product Requirements Document

**Document ID:** MC-PRD-001  
**Version:** 1.0  
**Baseline date:** 29 October 2026  
**Status:** Awaiting formal Product Owner sign-off  
**Project methodology:** Agile, one-week sprints  
**Development method:** Guided AI-assisted coding with full human review

---

## 1. Product Vision

MERN Commerce will be a single-vendor electronics shopping platform for customers in India.

Customers will be able to browse products, choose product variants, register and log in, manage carts and addresses, place Cash on Delivery orders, track fulfillment, cancel eligible orders, and submit return requests.

Store administrators will manage catalog information, inventory, delivery coverage, shipping charges, orders, COD collection, cancellations, and returns.

The first release is a functional portfolio demonstration. Real commercial transactions are not permitted until separate business and compliance approvals are complete.

## 2. Product Goals

1. Deliver a fully demonstrable customer purchasing workflow.
2. Deliver the administrative workflows necessary to operate the simulated store.
3. Demonstrate professional MERN development, Agile delivery, testing, and documentation practices.
4. Maintain clear business boundaries that permit a future commercial release without promising commercial readiness at MVP completion.

## 3. User Roles

**Visitor:** Browse, search, filter, and inspect products.

**Customer:** Register, authenticate, manage a cart and addresses, place COD orders, view orders, request eligible cancellations, and initiate returns.

**Administrator:** Manage products, variants, categories, inventory, delivery rules, orders, COD collection, returns, and refund records.

Administrator privileges must never be assigned through public self-registration.

## 4. MVP Functional Requirements

### FR-01 — Accounts

- Customer registration, login, and logout
- Secure authentication and role-based authorization
- Basic customer profile editing
- Saved delivery addresses
- Account-specific access to cart, orders, and return requests

### FR-02 — Electronics Catalog

- Product listing, searching, category filtering, and pagination
- Product details with specifications, brand, model, and warranty information
- Product images and availability
- Variants with unique SKUs, independent inventory, and variant-specific pricing
- Configurable product classification and required disclosure fields
- Administrator product and category management

### FR-03 — Shopping Cart

- Add, modify, and remove selected product variants
- Persistent authenticated cart
- Current price and stock validation
- Customer-visible cart subtotal and checkout error messages

### FR-04 — Delivery Serviceability

- PIN-code based eligibility
- Initial simulated coverage limited to selected Kerala PIN codes
- Separate COD eligibility configuration
- Serviceability checked before order creation
- Unsupported PIN codes blocked with a clear message
- Admin-controlled activation/deactivation of serviceability records

No demo serviceability record may be represented as confirmation from an actual courier.

### FR-05 — Shipping Calculation

- Standard shipping fee: ₹79
- Free shipping at merchandise subtotal ≥ ₹999
- Threshold applied to discounted, tax-inclusive merchandise subtotal
- No initial COD surcharge
- Shipping calculated and verified on the backend
- Final shipping amount preserved in confirmed orders

### FR-06 — Pricing and Tax

- Tax-inclusive product display pricing
- Configurable illustrative tax classifications and rules in demo mode
- No universally assumed electronics GST rate
- Correct separation of displayed price, component tax information, shipping charge, and order total
- Pricing/tax snapshots stored for historical orders
- Commercial tax invoices disabled until real seller details and tax rules are verified

### FR-07 — COD Checkout

- Authentication required
- Validate selected address and delivery eligibility
- Revalidate product variant, availability, price, and stock
- Calculate total payable server-side
- Display the final order summary before customer confirmation
- Prevent duplicate order creation
- Commit inventory and order operations consistently
- Return an order confirmation reference
- Initialize COD collection state as unpaid

### FR-08 — Orders

- Customer order history and order detail pages
- Administrator order overview and detail management
- Controlled fulfillment state transitions
- Distinct payment and fulfillment states
- Historical order and address snapshots
- Auditable status changes

### FR-09 — Cancellation

- Customer can request cancellation of an owned eligible order
- Eligible requests before packing are automatically approved
- Packed but unshipped requests enter administrator review
- Shipped/delivered orders follow appropriate refusal, return, or exception handling
- Approved cancellations restore relevant inventory exactly once
- Decisions and reasons are recorded

### FR-10 — Returns

- Customer may request an eligible return on a delivered order item
- Standard voluntary request window: seven calendar days after delivery
- Applicable statutory and warranty remedies remain available independently of that standard window
- Customer specifies item, quantity, reason, and optional evidence
- Administrator reviews and resolves requests
- Approved requests follow a manual pickup or customer-shipping arrangement
- Return receipt and inspection are recorded
- Returned stock is not automatically considered sellable
- Customer-visible status history is maintained

### FR-11 — COD Refunds

- Monetary refunds are not automatically transferred
- Authorized administrators record and process approved refunds manually
- The refund method, amount, reference, actor, and completion status are tracked
- Refunds remain pending until actual completion is verified
- Sensitive refund destination information is protected

For a portfolio demonstration, refund completion and payment references are simulated.

### FR-12 — Administration

- Manage electronics products, variants, categories, images, and stock
- Manage Kerala demo PIN-code eligibility
- Manage standard shipping charges and free-shipping threshold
- Manage permitted tax classification references
- Manage orders and COD collection states
- Review cancellations and return requests
- Record inventory inspection and disposition
- View basic operational metrics

## 5. Proposed Business State Models

### Fulfillment

Placed → Confirmed → Packed → Shipped → Delivered

Exceptional states include Cancelled and Delivery Failed.

### Payment

Unpaid → Collected

Exception or financial resolution states are separate from fulfillment.

### Return Requests

Requested → Under Review → Approved → In Transit → Received → Inspected → Resolved

Rejection, withdrawal, and failed-logistics paths must also be supported.

State changes must be validated by the backend and recorded with meaningful audit information.

## 6. MVP Acceptance Standard

The MVP is accepted only when:

- All mandatory P0 user stories satisfy their acceptance criteria.
- Authentication and ownership restrictions are verified.
- Product variant inventory cannot be oversold through concurrent checkout.
- Order creation prevents accidental duplicates.
- Shipping threshold and eligibility rules are tested.
- Tax-inclusive demo calculations do not double-charge tax.
- Cancellation and inventory restoration are consistent.
- Return handling and simulated refunds maintain traceable statuses.
- Critical integration and security tests pass.
- The Product Owner approves the demonstrated increment.

## 7. Non-Functional Requirements

- TypeScript across the MERN stack
- Modular, maintainable project structure
- Secure authentication, authorization, and password handling
- Backend validation and controlled error responses
- Data consistency for inventory and order operations
- Idempotent sensitive operations
- Appropriate indexing and pagination
- Responsive and accessible interfaces
- Structured logs and audit records
- Documented API contracts
- Automated testing
- Human review of AI-generated code

## 8. Excluded from MVP

- Real payment gateway integration
- Multi-vendor functionality
- Wishlist and customer ratings
- Coupon and loyalty engines
- Personalized recommendations
- Automated financial refunds
- Multi-warehouse stock management
- International shipping
- Native mobile applications
- Advanced accounting integrations

## 9. Release Boundaries

**Portfolio MVP:** Test products, simulated orders, illustrative taxation, fictional seller identity, manually simulated delivery and refund operations.

**Commercial Release:** Requires verified seller identity, tax/invoice configuration, actual inventory, logistics contracts, COD settlement arrangements, product compliance, privacy, consumer policies, security review, and operational support.

## 10. Change Control

After approval, any material scope or policy change must:

1. Be entered in the Product Backlog or change register.
2. Identify affected acceptance criteria and dependencies.
3. Be reviewed for impact.
4. Receive Product Owner approval before implementation.

## 11. Approval

**Business decisions:** Confirmed  
**MVP scope:** Proposed for approval  
**Product Backlog:** 31 identified user stories, subject to sprint refinement  
**Residual assumptions:** Documented separately  
**Product Owner signature:** Pending  
**Implementation authorization:** Not granted

No architecture or application-code generation is authorized by this draft.