
# Product Requirements Document (PRD)
## Billing & Inventory SaaS

**Version:** 1.0  
**Status:** Draft  
**Target Market:** India  
**Platforms:** Web SaaS + Android  
**Document Date:** October 2026

---

## 1. Product Overview

### 1.1 Vision

Build a modern, easy-to-use billing and inventory management SaaS that helps Indian businesses manage sales, GST invoices, inventory, customers, suppliers, payments, and business reports from one unified platform.

The product should be simple enough for small shop owners and scalable enough to support growing businesses with multiple employees and branches.

### 1.2 Mission

- Simplify daily business operations.
- Reduce manual bookkeeping and inventory errors.
- Make billing fast and reliable.
- Provide clear, actionable business insights.
- Offer affordable software for businesses of different sizes.
- Deliver a consistent experience across web and Android.

### 1.3 Product Principles

- Simplicity over unnecessary complexity.
- Accuracy and data integrity first.
- Security and privacy by design.
- Fast workflows for repetitive tasks.
- Comfortable long-duration usage.
- Mobile accessibility.
- Scalable, maintainable architecture.

---

## 2. Problem Statement

Small businesses often manage billing, stock, customer balances, supplier purchases, and reports through disconnected software, spreadsheets, or manual records.

This creates problems such as:

- Incorrect or outdated stock information.
- Time-consuming invoice creation.
- Difficulty tracking outstanding payments.
- Limited visibility into sales performance.
- Duplicate or inconsistent records.
- Weak employee access controls.
- Difficulty accessing business information remotely.

The product aims to bring these workflows together in one reliable platform.

These assumptions must be validated through customer interviews and competitor research before the final MVP scope is locked.

---

## 3. Target Audience

### 3.1 Potential Customer Segments

- Retail shops.
- Wholesalers.
- Distributors.
- Small trading businesses.
- General stores.
- Electronics and accessories shops.
- Clothing and footwear stores.
- Other product-selling small businesses.

### 3.2 User Roles

**Business Owner**
- Manage business settings.
- View business performance.
- Manage subscriptions and employees.
- Access authorized business records.

**Administrator / Manager**
- Manage day-to-day operations.
- Manage products, billing, and inventory.
- View reports according to permissions.

**Cashier / Billing Operator**
- Create invoices.
- Search products and customers.
- Record payments when authorized.

**Inventory Operator**
- Manage stock movements.
- Update product information when permitted.
- Perform stock adjustments.

**Accountant / Report Viewer**
- Review invoices and financial summaries.
- Export permitted reports.

### 3.3 Customer Validation

Before development is finalized:

- Interview small-business owners.
- Identify existing tools and major frustrations.
- Evaluate competitors such as Vyapar, myBillBook, and Zoho Inventory.
- Test willingness to pay.
- Identify the best initial customer segment.
- Validate whether offline billing is essential.

---

## 4. Product Goals

1. Provide reliable billing and inventory management.
2. Reduce the time required to create invoices.
3. Keep stock records consistent with business transactions.
4. Track customers, suppliers, and outstanding balances.
5. Present useful business reports.
6. Support multiple employees with customizable permissions.
7. Synchronize authorized business data across web and Android.
8. Offer a sustainable free-to-paid subscription model.
9. Establish a secure multi-tenant architecture.
10. Create a distinctive, professional user experience.

---

## 5. Initial MVP Scope

### 5.1 Authentication and Business Setup

- User registration and login.
- Account recovery.
- Business profile creation.
- Business contact and address details.
- Relevant GST identification details.
- Invoice numbering and business preferences.
- Employee invitations and access management.

### 5.2 Product Management

- Add, view, edit, archive, and search products.
- Product name and description.
- SKU or product code.
- Product category.
- Unit of measurement.
- Purchase cost and selling price.
- Applicable tax category and rate.
- Current recorded stock.
- Low-stock threshold.
- Product import and export where feasible.

### 5.3 Inventory Management

- Record opening stock.
- Record stock increases and decreases.
- Automatically update stock following finalized sales.
- Track stock movement history.
- Display current stock levels.
- Generate low-stock alerts.
- Record manual stock adjustments with reasons.
- Maintain an audit trail.
- Prevent unauthorized stock changes.

Negative stock should be blocked by default unless an explicitly authorized override is introduced.

### 5.4 Billing and Invoicing

- Create and edit draft invoices.
- Select or create customers.
- Add products and quantities.
- Apply supported discounts.
- Calculate taxable amounts and applicable taxes.
- Generate invoice numbers.
- Finalize invoices.
- Print and download invoices.
- Search and filter invoices.
- Record full and partial payments.
- Track unpaid and overdue balances.
- Support controlled cancellation and correction workflows.

GST calculations, invoice formats, and statutory requirements must be validated against applicable Indian regulations before production release.

### 5.5 Customer Management

- Create and update customer records.
- Store contact and billing details.
- Search customers.
- View customer invoice history.
- Track outstanding balances.
- View payment history.

### 5.6 Supplier Management

- Create and manage suppliers.
- Store supplier contact details.
- View supplier transaction history.
- Record purchases and stock receipts if included in the validated MVP.

### 5.7 Dashboard

Display:

- Today's sales.
- Sales over a selected period.
- Number of invoices.
- Outstanding customer balances.
- Low-stock products.
- Recent transactions.
- Recent stock movements.

### 5.8 Reports

Initial reports:

- Sales report.
- Invoice report.
- Inventory summary.
- Stock movement report.
- Customer outstanding report.
- Payment history.

Reports must reconcile with underlying transactions.

### 5.9 Android Application

Prioritize:

- Secure authentication.
- Dashboard.
- Product search.
- Stock lookup.
- Customer lookup.
- Invoice creation and viewing.
- Payment recording, where included in the MVP.
- Low-stock indicators.

Offline functionality, barcode scanning, and specialized printer integrations require separate validation and scope definition.

---

## 6. Functional Requirements

| ID | Requirement | Priority |
|---|---|---|
| FR-01 | Secure authentication and account recovery | P0 |
| FR-02 | Create and configure a business | P0 |
| FR-03 | Enforce business-level data isolation | P0 |
| FR-04 | Product CRUD and search | P0 |
| FR-05 | Stock ledger and movement history | P0 |
| FR-06 | Create and finalize invoices | P0 |
| FR-07 | Accurate invoice and tax calculations | P0 |
| FR-08 | Transactional stock deduction after sales | P0 |
| FR-09 | Record payments and outstanding balances | P0 |
| FR-10 | Customer management | P0 |
| FR-11 | Dashboard and essential reports | P0 |
| FR-12 | Role-based access control | P0 |
| FR-13 | Audit trail for critical actions | P0 |
| FR-14 | Printable and downloadable invoices | P0 |
| FR-15 | Supplier purchases and stock receipts | P1 |
| FR-16 | Product import and export | P1 |
| FR-17 | Core Android workflows | P0 for Android launch |
| FR-18 | Multi-branch management | P1 |
| FR-19 | Custom invoice branding | P1 |
| FR-20 | Advanced analytics | P2 |

**Priority definitions**

- P0: Essential for the initial release.
- P1: High-value feature after core workflows.
- P2: Future enhancement.

---

## 7. Core User Workflows

### 7.1 First-Time Setup

1. User creates an account.
2. User creates a business profile.
3. User configures business and invoice settings.
4. User adds products and opening stock.
5. User optionally adds customers and employees.
6. User reaches the dashboard.

### 7.2 Sales Workflow

1. Open a new invoice.
2. Select or create a customer.
3. Add products and quantities.
4. Calculate discounts, taxes, and totals.
5. Review the invoice.
6. Save as draft or finalize.
7. Validate permissions, stock, and business ownership.
8. Finalize the invoice and associated stock movements atomically.
9. Record payment if received.
10. Print, download, or share the invoice through supported capabilities.

### 7.3 Inventory Adjustment Workflow

1. Open a product's stock record.
2. Enter the adjustment quantity and reason.
3. Validate permissions and stock policy.
4. Record the stock movement.
5. Update the current stock summary.
6. Preserve the action in the audit trail.

### 7.4 Payment Workflow

1. Open a customer or invoice.
2. Review the outstanding amount.
3. Enter the payment amount and method.
4. Validate the payment.
5. Record the payment transaction.
6. Recalculate the remaining balance.
7. Display the updated payment history.

---

## 8. Business Rules and Data Integrity

- Every business-owned record must belong to the correct business.
- All reads and writes must enforce authorization.
- Monetary values must use exact decimal arithmetic.
- Tax and rounding rules must be consistent.
- Finalized invoices must not be silently edited.
- Invoice corrections must follow controlled reversal or correction workflows.
- Invoice numbers must be unique within the defined numbering scope.
- Stock changes must be represented by traceable movements.
- Invoice finalization and stock updates must be atomic.
- Retried requests must not create duplicate invoices or payments.
- Payment records must reconcile with invoice balances.
- Financial records must not be permanently deleted through ordinary user workflows.
- Critical actions must record the actor, timestamp, action, and relevant changes.
- Branch-specific numbering and inventory rules must be defined before multi-branch release.

---

## 9. Subscription and Pricing Model

Use a hybrid subscription model.

### Free Plan

- Essential billing functionality.
- Basic product and inventory management.
- Basic dashboard.
- Limited users or records, subject to validation.

### Premium Trial

- Temporary access to selected premium features.
- Clear trial expiration information.
- Easy transition to a paid plan.

### Paid Plans

Potential pricing dimensions:

- Business size.
- Number of employees.
- Number of branches.
- Advanced reporting.
- Higher transaction or record limits.
- Additional administrative features.

Exact prices, usage limits, and feature entitlements must be determined through market research and willingness-to-pay testing.

Subscription enforcement must happen on the backend, not only in the user interface.

---

## 10. Non-Functional Requirements

### 10.1 Security

- Enforce tenant isolation.
- Implement least-privilege permissions.
- Validate sensitive operations on the server.
- Use secure transport.
- Protect API keys and privileged secrets.
- Apply appropriate rate limits.
- Audit administrative actions.
- Define account deletion, data export, and retention policies.
- Prevent data exposure through searches, reports, logs, and exports.

### 10.2 Performance

Initial targets for testing:

- Target p95 API response time below 500 ms for common operations under expected load.
- Target dashboard loading within 2 seconds for typical small-business datasets on a reasonable connection.
- Use pagination for large datasets.
- Index frequently queried fields.
- Measure actual performance under realistic test conditions.

These targets are engineering goals, not guarantees.

### 10.3 Reliability

- Use database transactions for financial and inventory operations.
- Implement safe retries and idempotency.
- Configure automated backups.
- Test restoration procedures.
- Monitor application errors.
- Define recovery-point and recovery-time objectives before production launch.

### 10.4 Accessibility and Usability

- Clear navigation and consistent layouts.
- Readable text and adequate contrast.
- Keyboard navigation on web.
- Visible focus indicators.
- Responsive layouts.
- Clear loading, success, empty, and error states.
- Accessible labels for forms and controls.
- Respect reduced-motion preferences.
- Do not rely on color alone to communicate status.

### 10.5 Localization

- Primary market: India.
- Support INR formatting.
- Support Indian date and number conventions.
- Include applicable GST-related fields.
- Design for Indian addresses and state information.
- Consider regional-language support after user research.

---

## 11. UI/UX and Visual Identity

### 11.1 Design Direction

The interface should feel:

- Premium and professional.
- Warm and approachable.
- Modern rather than traditional.
- Visually distinctive without unnecessary decoration.
- Comfortable for users working throughout the day.
- Information-dense where operational workflows require it.

### 11.2 Official Color Palette

| Token | Hex |
|---|---|
| Dark Walnut | `#582F0E` |
| Saddle Brown | `#7F4F24` |
| Toffee Brown | `#936639` |
| Camel | `#A68A64` |
| Khaki Beige | `#B6AD90` |
| Dry Sage | `#C2C5AA` |
| Dry Sage 2 | `#A4AC86` |
| Dusty Olive | `#656D4A` |
| Ebony | `#414833` |
| Charcoal Brown | `#333D29` |

### 11.3 Color Usage

- Charcoal Brown: navigation and primary dark surfaces.
- Dark Walnut: selected primary actions and brand accents.
- Dusty Olive: secondary accents and selected navigation states.
- Dry Sage: subtle highlights and secondary panels.
- Khaki Beige and Camel: supporting accents and borders.
- Warm Ivory: additional neutral workspace background.
- White or near-white: cards, forms, and readable content surfaces.

Text and interactive controls must meet appropriate contrast requirements.

### 11.4 Typography

Recommended font system:

- **DM Sans:** Main interface, labels, forms, buttons, and tables.
- **Manrope:** Page headings, dashboard metrics, and section titles.
- **IBM Plex Mono:** Invoice identifiers, SKUs, and selected numerical data.

Use a clear typographic hierarchy and tabular numerals for aligned financial values.

### 11.5 Interaction Design

- Use subtle transitions and restrained animation.
- Keep frequent actions easy to reach.
- Avoid unnecessary modals and multi-step forms.
- Provide clear feedback after saving or finalizing transactions.
- Use skeletons or loading indicators for asynchronous operations.
- Support efficient keyboard-based data entry where appropriate.
- Default to a comfortable light theme; evaluate optional dark mode.

---

## 12. Proposed Technology Stack

The following is the proposed stack and must be validated during technical design.

### Web Application

- Next.js
- React
- TypeScript
- Tailwind CSS
- Accessible component primitives
- Lucide icons

### Android Application

- Flutter
- Dart

### Backend and Database

- Supabase
- PostgreSQL
- Supabase Auth
- Row Level Security (RLS)
- Database migrations and controlled server-side operations

### Development and Deployment

- Git and GitHub
- Automated tests and CI/CD
- Separate development, staging, and production environments
- Managed hosting selected after cost and deployment validation
- Monitoring, logging, backups, and recovery procedures

### Architecture Requirements

- Shared backend and business data for web and Android.
- Explicit tenant isolation.
- Centralized validation for critical business operations.
- Transaction-safe invoice and inventory processing.
- Versioned database migrations.
- Server-side enforcement of subscription limits.
- No privileged service keys in client applications.

---

## 13. High-Level Data Model

Proposed entities:

- Users
- Businesses
- Business Memberships
- Roles
- Permissions
- Business Settings
- Branches
- Products
- Product Categories
- Stock Balances
- Stock Movements
- Customers
- Suppliers
- Sales Invoices
- Invoice Items
- Payments
- Supplier Purchases
- Purchase Items
- Audit Logs
- Subscription Plans
- Business Subscriptions

Relationships, constraints, indexes, and transaction rules must be defined in the technical requirements document.

The schema must clearly distinguish business-level ownership from user identity. Tenant isolation must be enforced at the database/backend level.

---

## 14. Analytics and Success Metrics

### Product Adoption

- Number of registered businesses.
- Percentage completing business setup.
- Percentage creating their first invoice.
- Weekly and monthly active businesses.
- Active users per business.

### Product Engagement

- Invoices created per active business.
- Frequency of inventory updates.
- Use of reports.
- Customer and product records maintained.

### Business Performance

- Free-to-paid conversion rate.
- Trial-to-paid conversion rate.
- Monthly recurring revenue.
- Customer retention and churn.
- Support requests per active business.

### Reliability

- Invoice finalization failure rate.
- Duplicate transaction incidents.
- Stock reconciliation discrepancies.
- API response times.
- Service availability.
- Backup restoration test results.

Initial numeric success targets should be established after customer discovery and prototype testing.

---

## 15. Risks and Mitigation

| Risk | Mitigation |
|---|---|
| Building for too many business types | Validate one initial customer segment |
| Strong existing competitors | Identify a specific underserved workflow |
| Incorrect GST calculations | Validate rules with qualified tax expertise and automated tests |
| Inventory discrepancies | Use a traceable stock ledger and reconciliation |
| Cross-tenant data exposure | Enforce and test database-level tenant isolation |
| Scope becoming too large | Maintain explicit MVP boundaries |
| Poor adoption by non-technical users | Test usability with real business owners |
| Subscription pricing mismatch | Conduct willingness-to-pay research |
| Unreliable synchronization | Define conflict, retry, and idempotency rules |
| High operating costs | Monitor per-business infrastructure and support costs |

---

## 16. Development Phases

### Phase 1: Discovery and Validation

- Research competitors.
- Interview potential customers.
- Identify the initial customer segment.
- Validate critical workflows.
- Define MVP boundaries.

### Phase 2: Product and Technical Design

- Finalize PRD.
- Prepare technical requirements document.
- Create user flows and wireframes.
- Define database schema.
- Design authentication and authorization.
- Define invoice, tax, and stock transaction rules.

### Phase 3: Foundation

- Set up repositories and environments.
- Configure database and migrations.
- Implement authentication.
- Implement business membership and tenant isolation.
- Implement roles and permissions.
- Establish testing and deployment workflows.

### Phase 4: Core Web Application

- Business setup.
- Product catalogue.
- Inventory ledger.
- Customers.
- Invoice creation and finalization.
- Payment records.
- Dashboard and essential reports.

### Phase 5: Android Application

- Authentication.
- Dashboard.
- Product and customer lookup.
- Core invoice workflows.
- Payment features included in the approved scope.

### Phase 6: Quality Assurance

- Unit and integration tests.
- Tenant isolation and permission tests.
- Invoice calculation tests.
- Inventory reconciliation tests.
- Concurrency and retry tests.
- Performance and usability testing.
- Security review.

### Phase 7: Pilot and Launch

- Recruit pilot businesses.
- Collect usage feedback.
- Fix critical usability and reliability issues.
- Validate pricing.
- Prepare customer support and documentation.
- Release gradually and monitor performance.

---

## 17. MVP Acceptance Criteria

The MVP is ready for a controlled pilot when:

- Users can securely create accounts and businesses.
- Business data remains isolated between tenants.
- Authorized staff can manage products and customers.
- Stock movements are traceable and consistent.
- Users can create, finalize, retrieve, and print invoices.
- Invoice totals and applicable tax calculations pass defined tests.
- Finalizing an invoice updates stock exactly once.
- Payments and outstanding balances reconcile.
- Unauthorized actions are rejected server-side.
- Critical business actions are auditable.
- Core workflows are usable on the supported Android release.
- Backup and recovery procedures have been tested.
- Known limitations and applicable tax-related constraints are documented.

---

## 18. Open Decisions

The following decisions remain open:

1. Which customer segment should be prioritized first?
2. Is offline billing essential for the first release?
3. Should supplier purchasing be included in the initial MVP?
4. Which invoice and GST workflows are required for the initial segment?
5. What are the final subscription prices and usage limits?
6. Which Android features must launch alongside the web application?
7. Is multi-branch support required in the first release or only in the architecture?
8. Which hosting and deployment configuration best meets security and cost requirements?
9. What product name and domain should be used?
10. Which languages should be supported initially?

---

## 19. Final Product Direction

Build a focused, reliable billing and inventory product for Indian businesses, with a premium but approachable interface and a secure foundation for future expansion.

The MVP should prioritize:

1. Business setup and access control.
2. Product and inventory management.
3. Accurate billing and invoice generation.
4. Customer records and payment tracking.
5. Essential dashboards and reports.
6. A practical Android experience.

Do not expand into a complete ERP until customer research demonstrates that the additional workflows are necessary.

**Document status:** Draft. Requirements, tax workflows, pricing, and technology choices must be validated before production implementation.
