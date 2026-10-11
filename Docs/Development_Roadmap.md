
# Billing & Inventory SaaS — Development Roadmap

**Version:** 1.0
**Status:** Proposed
**Product:** Billing & Inventory SaaS
**Target Market:** Indian small businesses
**Platforms:** Web SaaS + Android
**Architecture Direction:** Next.js + TypeScript + Supabase/PostgreSQL + Flutter
**Business Model:** Free plan + premium trial + paid subscription tiers
**Primary Currency:** INR (₹)

---

## 1. Product Development Strategy

## 1.1 Objective

Build a reliable, user-friendly billing and inventory management product
that helps Indian small businesses:

- Create professional invoices.
- Manage products and stock.
- Track customer payments and outstanding balances.
- Monitor daily business activity.
- Reduce manual bookkeeping.
- Access business information from web and Android devices.
- Expand to multiple employees and branches as the business grows.

The product should be developed in small, testable releases rather than
attempting to build every planned feature simultaneously.

## 1.2 Core Development Principles

1. Build the smallest useful product first.
2. Validate real business workflows before adding advanced features.
3. Prioritize financial correctness and data security over visual complexity.
4. Build shared business rules into trusted backend operations.
5. Test tenant isolation from the beginning.
6. Maintain version-controlled database migrations.
7. Release working increments continuously.
8. Avoid premature microservices and unnecessary infrastructure.
9. Keep hosting and third-party service costs low during validation.
10. Collect feedback from real shop owners before expanding the scope.

---

## 2. Recommended Technology Stack

The following is the proposed stack. Reassess costs, deployment needs,
and developer productivity before locking in production decisions.

## Web Application

- **Framework:** Next.js
- **Language:** TypeScript
- **UI:** React
- **Styling:** Tailwind CSS
- **Components:** Accessible reusable component system
- **Forms:** React Hook Form
- **Validation:** Zod
- **Charts:** Recharts, when needed
- **Icons:** Lucide

## Backend and Database

- **Backend platform:** Supabase
- **Database:** PostgreSQL
- **Authentication:** Supabase Auth
- **Authorization:** PostgreSQL RLS + trusted server-side checks
- **File storage:** Supabase Storage or another suitable private object store
- **Database changes:** Version-controlled SQL migrations
- **Critical operations:** PostgreSQL transactions and
  narrowly scoped database functions

## Android Application

- **Framework:** Flutter
- **Language:** Dart
- **State management:** Riverpod
- **Navigation:** GoRouter
- **HTTP client:** Dio
- **Barcode scanning:** Add a suitable package after validating device support

## Development and Operations

- Git + GitHub
- VS Code or another compatible editor
- Local development environment
- Automated tests
- CI checks
- Production error monitoring
- Database backups and recovery testing

**Important:** Web and Android clients should use the same backend rules.
Do not duplicate financial or stock calculation logic independently in both
clients.

---

## 3. Overall Roadmap

| Phase | Name                                    | Estimated Duration |
| ----- | --------------------------------------- | ------------------ |
| 0     | Market Validation and Product Decisions |             1 week |
| 1     | Project Foundation and Design System    |             1 week |
| 2     | Database and Security Foundation        |          1–2 weeks |
| 3     | Authentication and Business Onboarding  |             1 week |
| 4     | Products and Inventory                  |          1–2 weeks |
| 5     | Customers and Billing                   |            2 weeks |
| 6     | Payments and Outstanding Balances       |             1 week |
| 7     | Dashboard and Reports                   |             1 week |
| 8     | Testing and Pilot Preparation           |          1–2 weeks |
| 9     | Web MVP Launch                          |             1 week |
| 10    | Android MVP                             |          2–3 weeks |
| 11    | Subscriptions and Monetization          |          1–2 weeks |
| 12    | Expansion and Optimization              |            Ongoing |

These estimates are planning ranges for a solo developer using
AI-assisted development. They are not guaranteed deadlines. Learning,
debugging, tax compliance, user feedback, and integration problems may
extend the schedule.

---

## 4. Phase 0 — Market Validation and Product Decisions

**Duration:** 1 week

## Phase 0 Objective

Validate the problem before investing heavily in implementation.

## Phase 0 Tasks

- [ ] Interview 10–15 small-business owners.
- [ ] Include a mix of retail shops and other suitable small businesses.
- [ ] Ask how they currently create bills.
- [ ] Ask how they track stock.
- [ ] Ask how they follow up on customer dues.
- [ ] Identify which tasks consume the most time.
- [ ] Learn what they dislike about existing tools.
- [ ] Observe the devices and languages they prefer.
- [ ] Ask whether they need GST invoicing.
- [ ] Understand their budget and willingness to pay.
- [ ] Identify the most common alternative: paper, spreadsheets, or existing software.
- [ ] Recruit 3–5 potential pilot businesses.

## Phase 0 Deliverables

- Customer interview notes
- Initial target customer segment
- Prioritized problem statement
- Competitor comparison
- MVP scope
- Initial pricing hypotheses

## Phase 0 Exit Criteria

Proceed when the team can explain:

- Who experiences the problem most acutely.
- What current workflow causes the greatest difficulty.
- Why the proposed solution would be better.
- Which businesses are willing to test an early version.

Do not interpret general interest as proof of willingness to pay.

---

## 5. Phase 1 — Project Foundation and Design System

**Duration:** 1 week

## Phase 1 Objective

Create the technical foundation and establish a consistent interface.

## Phase 1 Tasks

### Repository Setup

- [ ] Create a GitHub repository.
- [ ] Establish the web application structure.
- [ ] Add environment variable templates.
- [ ] Configure TypeScript.
- [ ] Configure linting and formatting.
- [ ] Create development and production environment conventions.
- [ ] Add a README with setup instructions.
- [ ] Configure basic CI checks.

### Visual Design System

Use the approved product palette:

```css
:root {
  --dark-walnut: #582f0e;
  --saddle-brown: #7f4f24;
  --toffee-brown: #936639;
  --camel: #a68a64;
  --khaki-beige: #b6ad90;
  --dry-sage: #c2c5aa;
  --dry-sage-2: #a4ac86;
  --dusty-olive: #656d4a;
  --ebony: #414833;
  --charcoal-brown: #333d29;
}
```

### Design Tasks

- [ ] Define typography.
- [ ] Define spacing, radius, and shadow tokens.
- [ ] Design the main navigation.
- [ ] Design buttons, inputs, dropdowns, and dialogs.
- [ ] Define loading, empty, success, and error states.
- [ ] Create responsive layouts.
- [ ] Check contrast and keyboard navigation.

## Phase 1 Deliverables

- Working repository
- Web app shell
- Shared design tokens
- Reusable UI components
- Development documentation

## Phase 1 Exit Criteria

The application starts locally, CI checks pass, and the main navigation
works on desktop and mobile-sized screens.

---

## 6. Phase 2 — Database and Security Foundation

**Duration:** 1–2 weeks

## Phase 2 Objective

Build the database before implementing business-critical workflows.

## Phase 2 Tasks

- [ ] Create the initial Supabase project.
- [ ] Set up local or isolated development configuration.
- [ ] Create version-controlled SQL migrations.
- [ ] Implement user profiles.
- [ ] Implement businesses and memberships.
- [ ] Implement branches and branch access.
- [ ] Implement products and categories.
- [ ] Implement customers.
- [ ] Implement inventory balances and stock movements.
- [ ] Implement invoices and invoice items.
- [ ] Implement invoice counters.
- [ ] Implement payments and allocations.
- [ ] Implement audit logs.
- [ ] Enable RLS on exposed tables.
- [ ] Add business-scoped foreign keys.
- [ ] Add indexes for expected query patterns.
- [ ] Create secure authorization helpers.
- [ ] Create automated database tests.

## Critical Security Tasks

- [ ] Test access with two separate businesses.
- [ ] Verify that one business cannot read another's data.
- [ ] Verify that branch restrictions are enforced.
- [ ] Restrict privileged operations.
- [ ] Ensure service-role secrets never reach client bundles.
- [ ] Protect financial tables against unauthorized mutations.
- [ ] Define a backup and recovery strategy.

## Phase 2 Deliverables

- Database migrations
- Initial entity relationships
- RLS policies
- Database authorization tests
- Documented local setup

## Phase 2 Exit Criteria

Business data isolation works, critical relationships are constrained,
and database changes can be recreated reliably from migrations.

**Do not proceed to real financial workflows until the security
foundation has been tested.**

---

## 7. Phase 3 — Authentication and Business Onboarding

**Duration:** 1 week

## Phase 3 Objective

Allow users to create accounts and establish a business workspace.

## Phase 3 Tasks

### Authentication

- [ ] Sign up
- [ ] Log in
- [ ] Log out
- [ ] Password recovery
- [ ] Session handling
- [ ] Protected routes
- [ ] Authentication error states

### Business Setup

- [ ] Business profile form
- [ ] Address and state
- [ ] GST registration status
- [ ] GSTIN input and appropriate validation
- [ ] Invoice preferences
- [ ] Default branch creation
- [ ] Onboarding checklist
- [ ] Business selector for users with multiple memberships

### Authorization

- [ ] Assign owner permissions through a trusted flow.
- [ ] Enforce business membership on the server.
- [ ] Protect administrative operations.
- [ ] Handle suspended or removed memberships.

## Phase 3 Deliverables

- Working authentication
- Business creation flow
- Business selection
- Protected application area

## Phase 3 Exit Criteria

A new user can create an account, set up a business, and access only
the business workspaces they are authorized to use.

---

## 8. Phase 4 — Products and Inventory

**Duration:** 1–2 weeks

## Phase 4 Objective

Implement reliable product management and stock tracking.

## Phase 4 Tasks

### Product Catalogue

- [ ] Add product
- [ ] Edit product
- [ ] Archive product
- [ ] Product search
- [ ] SKU support
- [ ] Barcode field
- [ ] Categories
- [ ] Units of measurement
- [ ] Selling price and purchase cost
- [ ] Product tax configuration
- [ ] Inventory tracking settings

### Inventory

- [ ] Opening stock
- [ ] Current stock display
- [ ] Stock adjustment form
- [ ] Adjustment reason
- [ ] Stock movement history
- [ ] Low-stock threshold
- [ ] Low-stock filters
- [ ] Stock reconciliation tools

### Integrity

- [ ] Implement a trusted stock-adjustment transaction.
- [ ] Lock balance rows during conflicting operations.
- [ ] Prevent invalid negative stock according to policy.
- [ ] Make stock movements auditable.
- [ ] Prevent duplicate stock changes on retries.

## Phase 4 Deliverables

- Product management screens
- Inventory list
- Stock adjustment workflow
- Stock ledger
- Low-stock alerts

## Phase 4 Exit Criteria

Authorized users can manage products and stock, and the stock balance
reconciles with recorded stock movements.

---

## 9. Phase 5 — Customers and Billing

**Duration:** 2 weeks

## Phase 5 Objective

Implement the central workflow: create and finalize invoices.

## Phase 5 Tasks

### Customer Management

- [ ] Add customer
- [ ] Edit customer
- [ ] Search customers
- [ ] Customer profile
- [ ] Customer invoice history
- [ ] Customer contact details
- [ ] GSTIN and address fields, where applicable

### Billing Interface

- [ ] Create invoice
- [ ] Select customer or walk-in customer
- [ ] Search products
- [ ] Add and remove line items
- [ ] Edit quantities
- [ ] Apply permitted discounts
- [ ] Calculate taxes
- [ ] Show subtotal and final total
- [ ] Save draft
- [ ] Edit draft
- [ ] Preview invoice

### Finalization

- [ ] Implement authoritative server-side calculations.
- [ ] Implement invoice numbering.
- [ ] Implement atomic invoice finalization.
- [ ] Deduct inventory transactionally.
- [ ] Preserve customer and business snapshots.
- [ ] Prevent ordinary edits to finalized invoices.
- [ ] Add invoice print and PDF generation.
- [ ] Add invoice search and filtering.

## Financial Integrity Requirements

- Use decimal arithmetic in the database and trusted calculation layer.
- Define tax and rounding policies.
- Protect against duplicate finalization requests.
- Prevent concurrent invoice-number collisions.
- Ensure invoice creation and stock deduction either succeed together or
  fail together.
- Preserve traceable cancellation and correction workflows.

## Phase 5 Deliverables

- Customer module
- Billing screen
- Invoice list and detail
- Finalized invoices
- Printable invoice output

## Phase 5 Exit Criteria

A user can create a valid invoice, finalize it exactly once, obtain a
unique invoice number, and produce the correct stock movement and
invoice totals.

GST workflows must be reviewed against current Indian requirements
before live commercial use.

---

## 10. Phase 6 — Payments and Outstanding Balances

**Duration:** 1 week

## Phase 6 Objective

Track payments and accurately show how much customers owe.

## Phase 6 Tasks

- [ ] Record cash payments.
- [ ] Record UPI payments.
- [ ] Record bank transfers.
- [ ] Record other supported payment methods.
- [ ] Support partial payments.
- [ ] Allocate payments to invoices.
- [ ] Display paid amount.
- [ ] Display outstanding balance.
- [ ] Display payment history.
- [ ] Implement payment reversals.
- [ ] Add idempotency protection.
- [ ] Add overdue invoice filters.
- [ ] Implement customer receivables view.

## Integrity Rules

- A recorded payment must not automatically imply that a digital payment
  was processed by the app.
- Payment allocations must not exceed the permitted amount.
- Duplicate requests must not create duplicate payments.
- Reversals must remain traceable.
- Outstanding balances must reconcile with invoices and payment allocations.

## Phase 6 Deliverables

- Record-payment form
- Payment history
- Outstanding balances
- Receivables list
- Payment audit events

## Phase 6 Exit Criteria

Full and partial payments work correctly, and invoice balances remain
consistent after payment recording and reversal.

---

## 11. Phase 7 — Dashboard and Reports

**Duration:** 1 week

## Phase 7 Objective

Give business owners a clear overview of daily operations.

## Phase 7 Tasks

### Dashboard

- [ ] Today's sales
- [ ] Outstanding receivables
- [ ] Total active products
- [ ] Low-stock products
- [ ] Recent invoices
- [ ] Recent payments
- [ ] Recent stock movements
- [ ] Quick actions

### Reports

- [ ] Sales by date range
- [ ] Sales by product
- [ ] Invoice summary
- [ ] Current stock report
- [ ] Low-stock report
- [ ] Stock movement report
- [ ] Outstanding invoice report
- [ ] Customer payment history

### Quality

- [ ] Add date filters.
- [ ] Add branch filters where applicable.
- [ ] Verify report calculations.
- [ ] Avoid unnecessary repeated database queries.
- [ ] Add pagination to large result sets.
- [ ] Restrict exports by user permissions.

## Phase 7 Deliverables

- Dashboard
- Sales reports
- Inventory reports
- Receivables reports

## Phase 7 Exit Criteria

Dashboard and reports display consistent, permission-scoped data that
reconciles with underlying records.

---

## 12. Phase 8 — Testing and Pilot Preparation

**Duration:** 1–2 weeks

## Phase 8 Objective

Prepare the web MVP for real-world testing.

## Testing Categories

### Functional Tests

- [ ] Authentication
- [ ] Business onboarding
- [ ] Product management
- [ ] Stock adjustment
- [ ] Invoice creation
- [ ] Invoice finalization
- [ ] Payment recording
- [ ] Reports

### Security Tests

- [ ] Cross-business data access
- [ ] Branch-level authorization
- [ ] Role restrictions
- [ ] Protected API operations
- [ ] File access permissions
- [ ] Environment secret exposure

### Financial Tests

- [ ] Discount calculations
- [ ] Tax calculations
- [ ] Rounding
- [ ] Partial payments
- [ ] Reversals
- [ ] Invoice numbering under concurrent requests
- [ ] Stock consistency
- [ ] Duplicate requests
- [ ] Cancellation and correction flows

### User Experience Tests

- [ ] Small-screen usability
- [ ] Empty states
- [ ] Slow network
- [ ] Error recovery
- [ ] Keyboard navigation
- [ ] Form validation
- [ ] Invoice printing

### Operational Tests

- [ ] Production build
- [ ] Environment configuration
- [ ] Logging and monitoring
- [ ] Database backups
- [ ] Restoration test
- [ ] Deployment rollback plan

## Pilot Plan

- [ ] Recruit 3–5 pilot businesses.
- [ ] Use synthetic data during initial QA.
- [ ] Obtain permission before importing real business data.
- [ ] Train pilot users.
- [ ] Observe real billing and stock workflows.
- [ ] Record failures and confusing screens.
- [ ] Fix critical issues before adding features.

## Phase 8 Exit Criteria

No known critical security or financial-integrity issues remain. Pilot
users can complete their main workflows with limited assistance.

---

## 13. Phase 9 — Web MVP Launch

**Duration:** Approximately 1 week after readiness criteria are met

## Phase 9 Objective

Release a controlled web version.

## Phase 9 Tasks

- [ ] Choose and configure hosting.
- [ ] Configure the production domain.
- [ ] Configure HTTPS.
- [ ] Set production environment variables.
- [ ] Apply reviewed database migrations.
- [ ] Verify production RLS policies.
- [ ] Enable appropriate backups.
- [ ] Configure error monitoring.
- [ ] Test account recovery.
- [ ] Test invoice printing on supported browsers.
- [ ] Publish privacy policy and terms.
- [ ] Document support and incident response.
- [ ] Release to pilot businesses.
- [ ] Monitor errors and user feedback.

## Launch Strategy

Begin with a controlled release rather than a large public launch.

Measure:

- Successful business onboarding
- Time to first product
- Time to first finalized invoice
- Invoice completion rate
- Weekly active businesses
- Billing and stock-related support requests
- Retention among pilot businesses

## Phase 9 Exit Criteria

The production system is stable enough for the pilot group, backup and
recovery procedures are documented, and major issues can be
investigated quickly.

---

## 14. Phase 10 — Android MVP

**Duration:** 2–3 weeks

## Phase 10 Objective

Deliver the most important workflows on Android after validating the
web backend.

## Initial Android Scope

- [ ] Login and logout
- [ ] Business selection
- [ ] Dashboard
- [ ] Product search
- [ ] Product details
- [ ] Customer search
- [ ] Create invoice
- [ ] Review invoice totals
- [ ] Finalize invoice
- [ ] Record payment
- [ ] View invoice details
- [ ] View stock
- [ ] View outstanding balances

## Mobile-Specific Requirements

- [ ] Touch-friendly forms
- [ ] Numeric keyboard for quantities and amounts
- [ ] Clear loading and saving states
- [ ] Safe request retries
- [ ] Session expiry handling
- [ ] Camera permission only when required
- [ ] Barcode scanning, if validated
- [ ] Error recovery on poor connections
- [ ] Android device testing
- [ ] Secure session and token handling

## Offline Scope

Do not promise full offline billing in the initial Android release.

Offline support should be a separate project because it requires
conflict resolution, synchronization, secure local storage, duplicate
protection, and authoritative invoice numbering.

## Phase 10 Exit Criteria

The Android app completes the selected workflows through the same
trusted backend and passes device, authorization, and transaction tests.

---

## 15. Phase 11 — Subscriptions and Monetization

**Duration:** 1–2 weeks

## Phase 11 Objective

Introduce the hybrid pricing model after the core product delivers real value.

## Planned Plans

### Free Plan

Potential capabilities:

- Basic billing
- Basic inventory
- Basic customer management
- Limited reports
- A reasonable usage limit

### Premium Trial

Potential capabilities:

- Temporary access to selected premium features
- Clear trial start and end dates
- Reminders before trial expiry

### Paid Plans

Potential differentiation:

- Higher invoice or product limits
- Additional staff
- Multiple branches
- Advanced reports
- Additional integrations
- Enhanced support

Final plan limits and pricing must be validated with customers.

## Phase 11 Tasks

- [ ] Define plan entitlements.
- [ ] Define feature and usage limits.
- [ ] Implement subscription state.
- [ ] Implement trial eligibility.
- [ ] Build plan comparison UI.
- [ ] Implement upgrade and downgrade handling.
- [ ] Integrate the selected payment provider.
- [ ] Verify payments through trusted provider callbacks.
- [ ] Make subscription updates idempotent.
- [ ] Handle payment failures and cancellations.
- [ ] Define post-expiry access policy.
- [ ] Test backend enforcement.

## Phase 11 Exit Criteria

The backend reliably grants and removes entitlements according to the
verified subscription state. Expiry or downgrade does not silently
delete customer business data.

---

## 16. Phase 12 — Expansion and Optimization

**Duration:** Ongoing

Only prioritize features that solve validated customer problems.

## Candidate Features

### Supplier and Purchase Management

- Supplier directory
- Purchase orders
- Goods receipt
- Supplier balances
- Purchase returns

### Multi-Branch Operations

- Branch inventory
- Branch-level staff access
- Stock transfers
- Branch reports

### Productivity

- CSV import/export
- Barcode scanning
- Invoice templates
- Bulk operations
- Better search

### Integrations

- WhatsApp invoice sharing
- Email notifications
- Accounting exports
- Payment-provider integrations
- Statutory integrations, where required

### Advanced Capabilities

- Inventory forecasting
- Profitability reports
- Customer insights
- Audit exports
- More granular permissions

## Prioritization Criteria

Score each feature using:

- Customer demand
- Business impact
- Development effort
- Maintenance cost
- Compliance risk
- Impact on existing workflows

Do not add a feature solely because a competitor has it.

---

## 17. Recommended Weekly Development Routine

For a solo developer, especially while studying, a sustainable routine
is better than attempting to finish the entire product in a few days.

### Suggested daily session

1. Review the current task.
2. Define one measurable outcome.
3. Implement a small change.
4. Run relevant tests.
5. Review the generated code.
6. Commit the working change.
7. Update documentation and the task checklist.

### Suggested weekly cycle

### Start of week

- Choose one milestone.
- Break it into small tasks.
- Identify risks and dependencies.

### During the week

- Implement and test incrementally.
- Avoid mixing unrelated features.
- Review security-sensitive code carefully.

### End of week

- Demonstrate the working feature.
- Fix important defects.
- Update the roadmap.
- Decide whether to continue or revise scope.

Use AI coding tools to accelerate implementation, but review
migrations, RLS policies, financial calculations, and transaction logic
yourself.

---

## 18. Development Workflow

Use this cycle for every feature:

```text
Requirement
    |
    v
Acceptance Criteria
    |
    v
UI / Flow Design
    |
    v
Database and Authorization Design
    |
    v
Implementation
    |
    v
Automated Tests
    |
    v
Manual Verification
    |
    v
Code Review
    |
    v
Commit and Documentation
    |
    v
Deploy to Test Environment
    |
    v
Verify and Release
```

For financial features, include failure and concurrency tests before
calling the feature complete.

---

## 19. Git Branching and Release Strategy

Suggested branch structure:

- `main` — production-ready code
- `develop` — integration branch, if needed
- `feature/*` — feature development
- `fix/*` — bug fixes
- `hotfix/*` — urgent production fixes

For a solo developer, a simpler workflow using `main` plus short-lived
feature branches is also acceptable.

## Commit Examples

- `feat(auth): add business onboarding`
- `feat(inventory): add stock adjustments`
- `feat(billing): implement invoice drafts`
- `feat(billing): finalize invoices transactionally`
- `feat(payments): record partial payments`
- `fix(inventory): prevent duplicate stock deduction`
- `test(security): verify business isolation`
- `docs: update development roadmap`

Never commit credentials, service-role keys, customer exports, or
production data.

---

## 20. Definition of Done

A feature is not complete merely because the UI looks correct.

Every feature must satisfy:

- [ ] Acceptance criteria are documented.
- [ ] Input validation exists.
- [ ] Authorization is enforced on the server.
- [ ] Business and branch scoping is correct.
- [ ] Database constraints support data integrity.
- [ ] Loading, success, and error states exist.
- [ ] Relevant automated tests pass.
- [ ] Failure and retry behavior is safe.
- [ ] Sensitive actions are audited where appropriate.
- [ ] No secrets are exposed.
- [ ] The UI is responsive and accessible.
- [ ] Documentation is updated.
- [ ] The feature is verified in a test environment.

---

## 21. MVP Launch Gate

The first public MVP should not launch until all critical requirements
below are satisfied.

## Product

- [ ] Business onboarding works.
- [ ] Products and customers can be managed.
- [ ] Invoices can be created and printed.
- [ ] Stock movements are accurate.
- [ ] Payments and outstanding balances reconcile.
- [ ] Core reports are consistent.

## Security

- [ ] Tenant isolation is tested.
- [ ] RLS is enabled and reviewed.
- [ ] Role restrictions are enforced.
- [ ] Secrets are protected.
- [ ] Critical operations are auditable.

## Reliability

- [ ] Invoice finalization is atomic.
- [ ] Stock cannot be silently corrupted.
- [ ] Duplicate financial operations are prevented.
- [ ] Backups and recovery are tested.
- [ ] Errors can be monitored and investigated.

## Business Readiness

- [ ] Pilot feedback has been reviewed.
- [ ] Pricing assumptions have been tested.
- [ ] Terms and privacy information are available.
- [ ] Customer support process exists.
- [ ] GST and invoice requirements have received appropriate review.

---

## 22. Success Metrics

## Activation

- Percentage of users completing business setup
- Percentage adding their first product
- Percentage creating their first finalized invoice

## Engagement

- Weekly active businesses
- Invoices created per active business
- Inventory updates per active business
- Repeat usage of core workflows

## Reliability Metrics

- Invoice finalization failure rate
- Duplicate transaction rate
- Stock reconciliation discrepancies
- Payment reconciliation discrepancies
- Application error rate

## Business

- Pilot-to-active conversion
- Free-to-paid conversion
- Subscription retention
- Support requests per active business
- Customer-reported time saved

Set numerical targets after collecting baseline data from pilot users.

---

## 23. Final Recommended Build Order

The recommended sequence is:

1. Validate the customer problem.
2. Finalize MVP requirements.
3. Set up the repository and design system.
4. Implement database schema and RLS.
5. Build authentication and business onboarding.
6. Build products and inventory.
7. Build customers.
8. Build draft and finalized invoices.
9. Implement GST calculation and invoice rendering.
10. Implement payment recording and outstanding balances.
11. Build dashboard and reports.
12. Run security, concurrency, and financial tests.
13. Pilot the web application.
14. Launch the web MVP.
15. Build the Android application.
16. Implement subscriptions.
17. Expand into supplier purchases, branches, and integrations.

**Final principle:** A smaller product that bills correctly, tracks
stock accurately, protects business data, and solves a real daily
problem is more valuable than a large application full of unfinished
features.

---

End of Development_Roadmap.md
