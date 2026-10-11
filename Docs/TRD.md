
# Technical Requirements Document (TRD)
## Billing & Inventory SaaS

**Version:** 1.0  
**Status:** Draft  
**Related Document:** `PRD.md`  
**Target Market:** India  
**Platforms:** Web SaaS + Android  
**Last Updated:** October 2026

---

## 1. Introduction

### 1.1 Purpose

This Technical Requirements Document defines the proposed architecture, technology stack, database structure, APIs, security requirements, business logic, testing strategy, and deployment approach for the Billing & Inventory SaaS.

It translates the product requirements in `PRD.md` into implementable technical specifications.

### 1.2 Technical Objectives

- Build a secure multi-tenant SaaS platform.
- Support web and Android clients through a shared backend.
- Maintain accurate billing, payment, and inventory records.
- Enforce customizable role-based access control.
- Ensure financial transactions are consistent and auditable.
- Support subscription-based monetization.
- Keep infrastructure affordable during early development.
- Allow the product to scale without requiring a complete rewrite.

### 1.3 Scope

This document covers:

- System architecture.
- Technology stack.
- Database design.
- Authentication and authorization.
- API conventions.
- Billing and inventory transaction processing.
- Subscription enforcement.
- Web and Android integration.
- Security, testing, deployment, and monitoring.

---

## 2. Technology Stack

The following is the proposed stack. Final choices must be validated before implementation.

### 2.1 Web Application

| Technology | Purpose |
|---|---|
| Next.js | Web application framework |
| React | Component-based UI |
| TypeScript | Type safety |
| Tailwind CSS | Styling |
| Accessible UI primitives | Consistent and accessible components |
| Lucide | Icons |
| React Hook Form | Form management |
| Zod | Client-side and shared schema validation |
| Recharts | Dashboard charts, if required |

### 2.2 Android Application

| Technology | Purpose |
|---|---|
| Flutter | Android application framework |
| Dart | Application programming language |
| Riverpod | State management |
| GoRouter | Navigation |
| Dio | HTTP networking |
| Secure storage | Sensitive local session data |

The Android app must use the same backend authorization and business rules as the web application.

### 2.3 Backend and Database

| Technology | Purpose |
|---|---|
| Supabase | Managed backend platform |
| PostgreSQL | Relational database |
| Supabase Auth | Authentication |
| PostgreSQL Row Level Security | Tenant isolation and data access control |
| SQL migrations | Version-controlled schema changes |
| PostgreSQL functions | Transaction-safe business operations |
| Supabase Storage | Private file storage when required |

Use server-side operations for sensitive workflows such as invoice finalization, payment recording, and stock adjustments.

### 2.4 Development and Deployment

- Git
- GitHub
- Automated testing
- GitHub Actions or equivalent CI/CD
- Separate development, staging, and production environments
- Managed hosting for the web application
- Managed PostgreSQL backups and monitoring
- Centralized error reporting and application logs

---

## 3. System Architecture

### 3.1 High-Level Architecture

```text
                 ┌──────────────────────┐
                 │     Web Browser      │
                 │  Next.js + TypeScript│
                 └──────────┬───────────┘
                            │
                            │ HTTPS
                            │
                 ┌──────────▼───────────┐
                 │   Shared Backend     │
                 │ Authentication       │
                 │ Authorization        │
                 │ Business Operations  │
                 │ Validation           │
                 └──────────┬───────────┘
                            │
                 ┌──────────▼───────────┐
                 │ Supabase / PostgreSQL│
                 │ RLS + Transactions   │
                 │ Business Data        │
                 └──────────────────────┘
                            ▲
                            │ HTTPS
                 ┌──────────┴───────────┐
                 │    Android App      │
                 │ Flutter + Dart      │
                 └─────────────────────┘
```

### 3.2 Architecture Principles

- Both clients share one backend and database.
- Authentication identifies the user; authorization determines what the user can do.
- Every business-owned record must be associated with a business or tenant.
- Sensitive business rules must be enforced server-side.
- PostgreSQL transactions must protect related financial and inventory changes.
- Database migrations must be version-controlled.
- Client applications must never contain privileged service-role credentials.
- External services must not bypass established authorization rules.

### 3.3 Multi-Tenant Model

Use a shared PostgreSQL database with tenant-scoped records.

Every business-owned table must include a `business_id`, directly or through a rigorously enforced relationship.

Access policies must verify that the authenticated user has an active membership in the relevant business and sufficient permissions for the requested operation.

Cross-tenant access must be denied by default.

---

## 4. Repository Structure

Recommended monorepo:

```text
billing-inventory-saas/
│
├── apps/
│   ├── web/
│   │   ├── app/
│   │   ├── components/
│   │   ├── features/
│   │   ├── hooks/
│   │   ├── lib/
│   │   ├── types/
│   │   └── tests/
│   │
│   └── android/
│       ├── lib/
│       │   ├── core/
│       │   ├── features/
│       │   ├── models/
│       │   ├── repositories/
│       │   ├── services/
│       │   └── widgets/
│       └── test/
│
├── supabase/
│   ├── migrations/
│   ├── seed.sql
│   ├── functions/
│   └── tests/
│
├── packages/
│   └── api-contracts/
│
├── docs/
│   ├── PRD.md
│   ├── TRD.md
│   ├── UI_UX.md
│   ├── DATABASE.md
│   └── API.md
│
├── .github/
│   └── workflows/
│
├── .env.example
├── .gitignore
└── README.md
```

The directory structure may evolve as implementation requirements become clearer.

---

## 5. Authentication and Authorization

### 5.1 Authentication

Use Supabase Auth for:

- Email and password authentication.
- Email verification where configured.
- Password recovery.
- Session management.
- Secure sign-out.
- Optional additional authentication methods in future releases.

The web and Android clients must use supported authentication SDKs and secure session-handling practices.

### 5.2 Business Membership

A user must have an active membership to access a business.

Membership data should include:

- User ID.
- Business ID.
- Assigned role.
- Membership status.
- Creation timestamp.
- Invitation or activation information where applicable.

A user's identity alone must never grant access to a business.

### 5.3 Role-Based Access Control

Proposed permissions include:

- `business.view`
- `business.manage`
- `users.view`
- `users.manage`
- `products.view`
- `products.manage`
- `inventory.view`
- `inventory.adjust`
- `customers.view`
- `customers.manage`
- `suppliers.view`
- `suppliers.manage`
- `invoices.view`
- `invoices.create`
- `invoices.finalize`
- `invoices.cancel`
- `payments.view`
- `payments.record`
- `reports.view`
- `reports.export`
- `subscriptions.manage`

These permissions must be evaluated on the server/database.

Roles should map to permission sets. The product must define safeguards to prevent accidental removal of the last authorized business owner.

---

## 6. Database Requirements

### 6.1 Database Standards

- Use PostgreSQL.
- Use UUID primary keys for major entities.
- Use `TIMESTAMPTZ` for timestamps.
- Use exact `NUMERIC` types for monetary values.
- Use foreign keys to enforce relationships.
- Use unique constraints for business-scoped identifiers.
- Add indexes for frequently queried fields.
- Use explicit transaction boundaries.
- Use database migrations for all schema changes.
- Avoid hard deletion of finalized financial records.

### 6.2 Core Tables

#### Identity and Business

- `profiles`
- `businesses`
- `business_memberships`
- `roles`
- `permissions`
- `role_permissions`
- `business_settings`
- `branches`

#### Products and Inventory

- `product_categories`
- `products`
- `stock_movements`
- `stock_balances` or an equivalent transactionally maintained summary

#### Customers and Suppliers

- `customers`
- `suppliers`

#### Sales and Payments

- `sales_invoices`
- `sales_invoice_items`
- `payments`
- `payment_allocations`
- `invoice_sequences`

#### Purchasing

- `purchase_invoices`
- `purchase_invoice_items`

#### Platform and Audit

- `audit_logs`
- `subscription_plans`
- `business_subscriptions`
- `usage_counters`
- `idempotency_keys`

Not every table must be included in the first migration. The final schema must follow the approved MVP scope.

### 6.3 Common Fields

Business-owned tables should generally include:

```text
id
business_id
created_at
updated_at
created_by
updated_by
```

Include only the fields appropriate to each entity. Use foreign keys, immutable history, and database policies to preserve integrity.

### 6.4 Product Fields

```text
id
business_id
category_id
sku
name
description
unit
purchase_price
selling_price
tax_category
tax_rate
track_inventory
low_stock_threshold
is_active
created_at
updated_at
```

Use exact decimal representations for prices and tax rates. SKU uniqueness should be defined within the business or branch scope, depending on the finalized requirements.

### 6.5 Stock Movement Fields

```text
id
business_id
product_id
branch_id
movement_type
quantity_delta
reference_type
reference_id
reason
created_by
created_at
```

The stock movement ledger should be the authoritative history of quantity changes.

The application must define how opening stock, purchases, sales, returns, adjustments, and cancellations affect inventory.

### 6.6 Sales Invoice Fields

```text
id
business_id
branch_id
customer_id
invoice_number
invoice_status
issue_date
due_date
currency
subtotal
discount_total
taxable_total
tax_total
grand_total
amount_paid
balance_due
notes
created_by
finalized_at
created_at
updated_at
```

Store finalized financial values as transaction records rather than recalculating historical invoices from mutable product settings.

### 6.7 Invoice Item Fields

```text
id
business_id
invoice_id
product_id
description
sku_snapshot
quantity
unit_price
discount_amount
tax_rate
taxable_amount
tax_amount
line_total
created_at
```

Historical invoice lines must retain the product description, price, and tax information used at finalization.

### 6.8 Payment Fields

```text
id
business_id
customer_id
payment_reference
payment_method
amount
currency
payment_date
status
recorded_by
created_at
```

Use payment allocations to associate payments with invoices, including partial payments. Define how unallocated customer credit is handled if that capability is introduced.

### 6.9 Database Constraints

Implement appropriate:

- Foreign key constraints.
- Positive quantity and amount checks where applicable.
- Valid status constraints.
- Business-scoped uniqueness.
- Non-negative balance rules where appropriate.
- Referential integrity for invoice items and payments.
- Idempotency constraints for retryable operations.

Do not rely solely on frontend validation.

---

## 7. Billing and Inventory Transaction Processing

### 7.1 Invoice Finalization

Invoice finalization must be a server-controlled transactional operation.

The operation must:

1. Authenticate the caller.
2. Verify business membership and permissions.
3. Validate invoice status and required fields.
4. Validate product ownership and current business rules.
5. Validate applicable pricing, tax, and rounding rules.
6. Enforce the configured stock policy.
7. Allocate a unique invoice number safely.
8. Persist final invoice and line-item values.
9. Create associated stock movements.
10. Update any stock summary maintained for performance.
11. Record the audit event.
12. Commit all changes together.

If any required step fails, the transaction must roll back.

Repeated requests must not create duplicate invoices or stock movements.

### 7.2 Inventory Calculations

For a product and branch:

```text
Current Stock =
Opening Stock
+ Stock Receipts
+ Customer Returns
+ Positive Adjustments
- Finalized Sales
- Supplier Returns
- Negative Adjustments
```

The exact movement types and return rules must be finalized in the database design.

Stock balances must reconcile with the stock movement ledger.

### 7.3 Payment Recording

Payment recording must:

1. Verify business membership and permissions.
2. Validate the amount and payment details.
3. Prevent duplicate processing of retried requests.
4. Create the payment record.
5. Allocate the payment to one or more invoices as supported.
6. Update outstanding balances transactionally.
7. Record an audit event.

Recorded payments must not be silently overwritten. Corrections should use a controlled reversal or adjustment workflow.

### 7.4 Monetary Precision

- Use PostgreSQL `NUMERIC` for money and tax calculations.
- Define currency precision and rounding rules centrally.
- Avoid JavaScript or Dart floating-point arithmetic for authoritative totals.
- Recalculate and validate authoritative invoice totals on the server.
- Ensure client and server calculations agree within the documented rounding rules.

### 7.5 Idempotency

Use idempotency keys for retry-sensitive operations such as:

- Invoice finalization.
- Payment recording.
- Stock adjustments.
- Other operations that create financial or inventory effects.

Store the operation identity and result under a suitable unique constraint. Define key scope, expiration, and behavior when the same key is reused with a different request.

---

## 8. API and Backend Requirements

### 8.1 API Principles

- Use HTTPS.
- Authenticate every protected request.
- Validate inputs server-side.
- Apply tenant and role checks.
- Return consistent error formats.
- Support pagination for large collections.
- Avoid leaking sensitive database details.
- Document request and response schemas.
- Apply rate limits to sensitive endpoints.

Use Supabase SDK operations for ordinary data access where safe. Use controlled server-side endpoints or database functions for privileged, multi-step, or transactional operations.

### 8.2 Core Operations

#### Authentication

```text
Supabase Auth SDK:
- Sign up
- Sign in
- Sign out
- Recover account
- Refresh session
```

#### Business

```text
GET    /api/businesses
POST   /api/businesses
GET    /api/businesses/:businessId
PATCH  /api/businesses/:businessId
```

#### Products

```text
GET    /api/products
POST   /api/products
GET    /api/products/:productId
PATCH  /api/products/:productId
```

#### Inventory

```text
GET    /api/inventory
GET    /api/inventory/movements
POST   /api/inventory/adjustments
```

#### Customers

```text
GET    /api/customers
POST   /api/customers
GET    /api/customers/:customerId
PATCH  /api/customers/:customerId
```

#### Invoices

```text
GET    /api/invoices
POST   /api/invoices
GET    /api/invoices/:invoiceId
PATCH  /api/invoices/:invoiceId
POST   /api/invoices/:invoiceId/finalize
POST   /api/invoices/:invoiceId/cancel
```

#### Payments

```text
GET    /api/payments
POST   /api/payments
GET    /api/invoices/:invoiceId/payments
```

These are logical endpoint contracts, not a requirement to implement every operation as a separate HTTP route. Final endpoint design should avoid duplicate business logic across clients.

### 8.3 Response Format

Example successful response:

```json
{
  "data": {
    "id": "resource-uuid"
  },
  "error": null
}
```

Example error response:

```json
{
  "data": null,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "The supplied data is invalid"
  }
}
```

Use appropriate HTTP status codes. Do not expose stack traces, secrets, or internal database details to clients.

### 8.4 Pagination

Support limit and cursor-based or offset-based pagination according to the endpoint's requirements.

Return pagination metadata where appropriate. Use stable sorting and indexes to avoid missing or duplicated records when practical.

---

## 9. Row Level Security and Tenant Isolation

### 9.1 Mandatory Rules

- Enable RLS on exposed business-data tables.
- Deny access unless an explicit policy permits it.
- Verify active membership in the requested business.
- Check permissions for sensitive operations.
- Enforce business ownership on inserts and updates.
- Protect child records through their parent relationships.
- Apply equivalent protections to views and database functions.
- Avoid security-definer functions unless their privileges and search paths are carefully controlled.

### 9.2 Policy Testing

Automated tests must verify:

- Business A cannot read Business B's products.
- Business A cannot update Business B's invoices.
- A user cannot create a record for a business they do not belong to.
- A cashier cannot perform owner-only actions.
- An inactive member cannot access business data.
- Invoice items cannot reference another business's invoice.
- Reports and exports respect the same tenant boundaries.

Never treat an unpredictable UUID as a substitute for authorization.

---

## 10. Frontend Requirements

### 10.1 Web Application

- Responsive layouts.
- Reusable UI components.
- Centralized API and error handling.
- Form validation.
- Loading, empty, success, and error states.
- Permission-aware navigation.
- Server-side authorization for sensitive operations.
- Accessible keyboard navigation.
- Search, sorting, and pagination for large tables.
- Print-friendly invoice templates.

Hiding a button is not a security control. Every protected operation must be enforced by the backend.

### 10.2 Android Application

- Feature-based architecture.
- Centralized API client.
- Secure session storage.
- Consistent loading and error handling.
- Input validation.
- Accessible touch targets.
- Responsive layouts for supported devices.
- Safe retry behavior for network failures.
- Clear synchronization status if offline support is introduced.

Offline writes must not be enabled until conflict resolution, idempotency, and synchronization behavior are explicitly designed.

### 10.3 State Management

Use a predictable state-management approach on each platform.

- Keep server data distinct from temporary UI state.
- Invalidate or refresh stale data after successful mutations.
- Avoid duplicating authoritative business calculations in multiple places.
- Handle session expiration gracefully.
- Avoid storing sensitive business information unnecessarily on devices.

---

## 11. File Storage and Invoice Documents

### 11.1 Storage

Use private object storage for files that require persistent storage.

Examples:

- Business logos.
- Uploaded product images, if required.
- Generated invoice documents, if persistence is necessary.
- Other business attachments introduced later.

### 11.2 Access Control

- Keep private business documents in private buckets.
- Validate business membership before issuing access.
- Use short-lived signed URLs where appropriate.
- Restrict file type and size.
- Never assume a file path proves authorization.

### 11.3 Invoice Generation

Invoice output must:

- Match the finalized invoice record.
- Use stored line-item and tax snapshots.
- Display the required business and customer information.
- Apply consistent number/date formatting.
- Support printing and PDF output.
- Avoid regenerating historical totals from current product prices.

Tax-specific invoice fields must be reviewed against applicable Indian requirements before release.

---

## 12. Subscription and Usage Enforcement

### 12.1 Subscription Model

Support:

- Free plan.
- Time-limited premium trial.
- Multiple paid plans.
- Plan-specific usage limits and entitlements.

### 12.2 Entitlements

Potential entitlement dimensions:

- Number of users.
- Number of branches.
- Number of products.
- Monthly invoice volume.
- Reporting features.
- Data export features.
- Advanced inventory capabilities.

The final limits must be based on market validation.

### 12.3 Enforcement

- Store subscription status in trusted backend records.
- Check entitlements on the server.
- Prevent client-side manipulation of usage limits.
- Define behavior for expired trials and failed renewals.
- Preserve customer data when a plan expires.
- Provide clear upgrade and downgrade workflows.

Payment gateway integration is outside the initial scope until the business model and provider are selected.

---

## 13. Security Requirements

### 13.1 Secrets Management

- Never commit production secrets.
- Keep `.env` files out of Git.
- Maintain a safe `.env.example`.
- Use hosting-provider secret management.
- Rotate credentials when exposed.
- Never ship Supabase service-role keys in frontend or Android builds.

### 13.2 Input Validation

Validate:

- IDs and business relationships.
- Quantities and prices.
- Tax rates and discount values.
- Invoice statuses.
- Payment amounts.
- File types and sizes.
- Pagination parameters.
- User permissions.

### 13.3 Operational Security

- Apply rate limits to authentication and sensitive operations.
- Record security-relevant events.
- Minimize personal data in logs.
- Review dependencies for known vulnerabilities.
- Maintain separate development and production environments.
- Restrict administrative access.
- Establish an incident response process.

### 13.4 Privacy

- Collect only necessary data.
- Document data retention.
- Support appropriate account and data export/deletion workflows.
- Protect backups.
- Define procedures for responding to suspected data exposure.
- Review applicable Indian privacy and data protection obligations before launch.

---

## 14. Performance and Scalability

### 14.1 Initial Performance Targets

These are targets to validate, not guarantees:

- p95 API latency below 500 ms for common operations under expected load.
- Typical dashboard load below 2 seconds on a reasonable connection.
- Indexed queries for common filtering and sorting.
- Paginated invoice, customer, and product lists.
- Responsive invoice finalization under normal conditions.

### 14.2 Scaling Strategy

- Begin with a managed PostgreSQL service.
- Use indexes based on measured query patterns.
- Avoid unnecessary database round trips.
- Paginate large collections.
- Use server-side aggregation for appropriate reports.
- Cache only where consistency requirements permit.
- Move expensive exports or reports to background jobs when needed.
- Monitor database connections and query performance.

Do not introduce microservices before actual scaling needs justify the added complexity.

---

## 15. Error Handling and Observability

### 15.1 Error Handling

The system must handle:

- Network failures.
- Authentication expiration.
- Validation errors.
- Permission denials.
- Duplicate requests.
- Stock conflicts.
- Database transaction failures.
- Subscription limit violations.
- File-generation errors.

Messages should explain the next appropriate action without exposing internal implementation details.

### 15.2 Monitoring

Track:

- API errors and latency.
- Invoice finalization failures.
- Payment processing errors.
- Stock reconciliation discrepancies.
- Database performance.
- Authentication failures.
- Background job failures, if introduced.
- Subscription entitlement failures.

Avoid logging passwords, access tokens, full payment credentials, or unnecessary personal information.

---

## 16. Testing Strategy

### 16.1 Unit Tests

Test:

- Monetary calculations.
- Tax and rounding rules.
- Discount calculations.
- Stock calculations.
- Invoice status transitions.
- Payment allocations.
- Subscription entitlements.
- Permission checks.

### 16.2 Integration Tests

Test:

- Authentication and business membership.
- Database constraints.
- RLS policies.
- Invoice finalization.
- Payment recording.
- Stock adjustments.
- Invoice cancellation and reversal.
- Retry and idempotency behavior.

### 16.3 End-to-End Tests

Test complete workflows:

- Business registration and setup.
- Product creation.
- Opening stock entry.
- Invoice creation and finalization.
- Payment recording.
- Stock reconciliation.
- Report generation.
- Unauthorized cross-tenant access.

### 16.4 Concurrency Tests

Verify that:

- Two users cannot allocate the same invoice number.
- Concurrent sales cannot silently violate stock policy.
- Retried finalization does not duplicate stock movements.
- Duplicate payment submissions do not create multiple payments.
- Concurrent updates preserve financial consistency.

### 16.5 Release Gate

No release should proceed with unresolved critical security issues, cross-tenant data leaks, duplicate financial transactions, or material invoice calculation errors.

---

## 17. CI/CD and Deployment

### 17.1 Environments

Maintain separate:

- Development.
- Staging.
- Production.

Use separate credentials and configuration for each environment.

### 17.2 CI Pipeline

Recommended pipeline:

1. Install dependencies.
2. Run formatting and lint checks.
3. Run type checks.
4. Run unit tests.
5. Run integration tests where configured.
6. Build the web application.
7. Validate database migrations.
8. Deploy to staging.
9. Run smoke tests.
10. Promote to production after required checks and approval.

### 17.3 Database Migrations

- Store migrations in version control.
- Review destructive changes.
- Test migrations against representative data.
- Use backward-compatible changes when possible.
- Define recovery procedures for failed migrations.
- Do not make undocumented manual production schema changes.

### 17.4 Backups and Recovery

- Configure automated database backups.
- Define recovery-point and recovery-time objectives.
- Test restoration periodically.
- Restrict access to backup data.
- Document recovery procedures.
- Verify the recovery of critical business records.

---

## 18. Environment Variables

Example `.env.example`:

```dotenv
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=

SUPABASE_SERVICE_ROLE_KEY=

NEXT_PUBLIC_APP_URL=
```

Rules:

- The public Supabase URL and publishable/anonymous client key may be exposed according to the selected Supabase configuration and security policies.
- The service-role key is server-only and must never be exposed to browsers, mobile apps, or client bundles.
- Add server-only environment checks.
- Never commit actual secret values.
- Use the current Supabase publishable-key conventions where supported.

Additional secrets should be introduced only when the corresponding service is implemented.

---

## 19. Implementation Phases

### Phase 1: Technical Foundation

- Initialize the repository.
- Configure Next.js and TypeScript.
- Initialize Flutter.
- Configure Supabase.
- Create initial migrations.
- Establish environment management.
- Configure automated checks.

### Phase 2: Identity and Tenant Isolation

- Implement authentication.
- Implement business profiles.
- Implement business memberships.
- Define roles and permissions.
- Enable RLS.
- Add tenant-isolation tests.

### Phase 3: Products and Inventory

- Implement categories and products.
- Implement opening stock.
- Implement stock movements.
- Implement stock summaries.
- Implement adjustments and reconciliation.

### Phase 4: Billing and Payments

- Implement invoice drafts.
- Implement invoice numbering.
- Implement authoritative calculations.
- Implement finalization transactions.
- Implement payment records and allocations.
- Implement invoice printing/PDF output.

### Phase 5: Customers and Reporting

- Implement customer records.
- Implement outstanding balances.
- Implement dashboard queries.
- Implement sales and stock reports.

### Phase 6: Android

- Implement authentication.
- Implement core product and customer workflows.
- Implement approved billing workflows.
- Add retry handling and error states.
- Test supported Android devices.

### Phase 7: Hardening and Pilot

- Perform security testing.
- Test transaction concurrency.
- Validate tax-related workflows.
- Test backup restoration.
- Run pilot business workflows.
- Measure performance.
- Fix critical issues before launch.

---

## 20. Technical Acceptance Criteria

The technical implementation is ready for a controlled pilot when:

- Authentication works on web and Android.
- Tenant isolation is verified by automated tests.
- Server-side permissions are enforced.
- Products and stock movements are consistent.
- Invoice finalization is atomic and retry-safe.
- Monetary calculations use exact decimal arithmetic.
- Invoice numbering is safe under concurrent requests.
- Payments and balances reconcile.
- Critical actions are auditable.
- Sensitive keys are not present in client builds.
- Automated tests run in CI.
- Database migrations are version-controlled.
- Backup restoration has been tested.
- Monitoring and error reporting are configured.
- Documented release checks pass.

---

## 21. Open Technical Decisions

1. Confirm whether Next.js and Flutter are the final frameworks.
2. Decide whether business operations use Supabase Edge Functions, server-side application routes, PostgreSQL functions, or a combination.
3. Finalize the tenant and membership schema.
4. Finalize customizable roles and permissions.
5. Define the invoice numbering scope.
6. Define stock reservation, negative-stock, returns, and cancellation rules.
7. Define tax calculation and rounding behavior.
8. Decide whether offline Android workflows are required.
9. Finalize hosting, backups, monitoring, and cost limits.
10. Define subscription billing and payment-provider integration when required.

---

## 22. Final Technical Direction

Build a modular monolithic SaaS using a shared backend and PostgreSQL database, with Next.js for the web application and Flutter for Android if these choices pass technical validation.

Prioritize:

1. Tenant isolation and authorization.
2. Transaction-safe billing and inventory.
3. Reliable monetary calculations.
4. Auditability.
5. Maintainable code and migrations.
6. Automated testing.
7. Affordable infrastructure.
8. A clear path to multi-branch and subscription capabilities.

The technical foundation must prioritize correctness and security over premature complexity.

**Document status:** Draft. The final schema, API contracts, GST workflows, infrastructure configuration, and operational limits must be reviewed before production implementation.
