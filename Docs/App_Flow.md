# AppFlow

## Billing & Inventory SaaS — Application Flow Specification

**Document status:** Draft v1.0
**Platforms:** Web SaaS + Android
**Target market:** Indian small businesses
**Business model:** Free plan + premium trial + multiple paid subscription tiers
**Primary goal:** Make billing, inventory tracking, and business management simple enough for everyday use.

---

## 1. Application Overview

The application helps small businesses manage their daily operations from one place.

### Core modules

1. Authentication and onboarding
2. Business profile and GST configuration
3. Dashboard
4. Billing and invoicing
5. Products and inventory
6. Customers
7. Suppliers and purchases
8. Payments and outstanding balances
9. Reports and analytics
10. Staff and permissions
11. Branch management
12. Subscription and billing
13. Settings and audit history

### Main navigation

**Web application**

- Dashboard
- Sales & Invoices
- Products & Inventory
- Customers
- Suppliers & Purchases
- Payments
- Reports
- Staff & Branches
- Settings

**Android application**

- Home
- Billing
- Inventory
- Customers
- More

The Android interface should prioritize quick actions, mobile billing, barcode scanning where supported, and stock updates.

---

## 2. High-Level User Journey

```text
Open Application
       |
       v
Welcome Screen
       |
       v
Sign Up / Log In
       |
       v
Email Verification (when required)
       |
       v
Check Existing Business Membership
       |
       +---- Existing Business ----> Select Business
       |                                  |
       +---- No Business -----------------+
                                          |
                                          v
                                  Business Setup
                                          |
                                          v
                                  GST Configuration
                                          |
                                          v
                                  Add First Products
                                          |
                                          v
                                  Invite Staff (Optional)
                                          |
                                          v
                                  Dashboard
                                          |
                    +---------------------+--------------------+
                    |                     |                    |
                    v                     v                    v
               Create Bill          Manage Stock         View Reports
                    |                     |                    |
                    v                     v                    v
              Record Payment        Stock Adjustment       Insights
```

---

## 3. Authentication Flow

### 3.1 Sign Up

```text
Welcome Screen
      |
      v
Create Account
      |
      v
Enter Name, Email, Password
      |
      v
Validate Input
      |
      v
Create Account
      |
      v
Email Verification (if required)
      |
      v
Check Business Membership
      |
      +---- Membership Found ----> Business Dashboard
      |
      +---- No Membership --------> Create / Join Business
```

### 3.2 Log In

1. User enters email and password.
2. System validates credentials.
3. Authentication service establishes a session.
4. System checks the user's active business memberships.
5. If one business exists, open it automatically.
6. If multiple businesses exist, show a business selector.
7. Redirect the user to the correct screen according to their role.

### 3.3 Password Recovery

```text
Login
  |
  v
Forgot Password
  |
  v
Enter Registered Email
  |
  v
Send Recovery Link
  |
  v
Verify Recovery Request
  |
  v
Set New Password
  |
  v
Return to Login
```

### Error states

- Invalid credentials
- Expired verification link
- Expired or invalid recovery link
- Network failure
- Account temporarily restricted
- No business access

Errors should be clear and actionable without revealing whether an arbitrary email address is registered.

---

## 4. Business Onboarding Flow

### Step 1: Business Details

Collect:

- Business name
- Business type
- Owner or administrator name
- Phone number
- Business email, optional
- Business address
- State and PIN code
- Preferred language and time zone

**Action:** Continue to GST setup.

### Step 2: GST Configuration

Ask the user to choose the applicable configuration:

- GST-registered business
- Unregistered business
- Other applicable tax configuration

For registered businesses, collect:

- GSTIN
- Registered business name, if different
- State of registration
- Invoice details

Validate GSTIN format and clearly flag any details that require external verification.

Do not assume every business is GST-registered or apply the same tax treatment to every product.

### Step 3: Invoice Preferences

Collect:

- Invoice prefix
- Starting invoice number, where appropriate
- Business logo, optional
- Default payment terms
- Invoice footer
- Tax display preferences
- Default document format

Invoice numbering must be unique and concurrency-safe within the applicable business or branch configuration.

### Step 4: Initial Inventory

Offer three choices:

1. Add products manually.
2. Import products using a supported CSV template.
3. Skip and add products later.

Product details may include:

- Product name
- SKU or barcode
- Category
- Unit of measurement
- Selling price
- Purchase cost
- Tax configuration
- Opening stock
- Low-stock threshold

Opening stock should be recorded as an auditable opening-stock movement.

### Step 5: Invite Staff (Optional)

- Enter staff email or phone, depending on supported invitation methods.
- Assign a predefined role.
- Send invitation.
- Allow the owner to skip this step.

### Step 6: Completion

Show an onboarding checklist:

- [ ] Business profile completed
- [ ] Tax settings reviewed
- [ ] First product added
- [ ] First customer added
- [ ] First invoice created

**Action:** Go to Dashboard.

---

## 5. Dashboard Flow

The dashboard provides a quick summary of the business's current state.

### Main sections

**Summary cards**

- Today's sales
- Outstanding receivables
- Total products
- Low-stock items

**Action shortcuts**

- Create invoice
- Add product
- Add customer
- Record payment
- Adjust stock

**Activity**

- Recent invoices
- Recent stock movements
- Recent payments

**Alerts**

- Products below their stock thresholds
- Overdue customer balances
- Draft invoices awaiting completion
- Subscription or account notices

### Dashboard interactions

```text
Dashboard
   |
   +--> Create Invoice ------> Billing Flow
   |
   +--> Low Stock -----------> Inventory Filter
   |
   +--> Outstanding ---------> Receivables List
   |
   +--> Recent Invoice -------> Invoice Details
   |
   +--> Sales Summary -------> Reports
   |
   +--> Quick Add Product ---> Product Form
```

All dashboard figures must use the active business and authorized branch scope.

Sales totals, payments received, and outstanding balances must be defined separately to avoid misleading financial summaries.

---

## 6. Billing and Invoice Flow

### 6.1 Create Invoice

```text
Dashboard
    |
    v
Sales & Invoices
    |
    v
Create Invoice
    |
    v
Select Customer / Walk-in Customer
    |
    v
Add Products or Services
    |
    v
Set Quantities
    |
    v
Calculate Prices, Discounts and Taxes
    |
    v
Validate Stock and Invoice Details
    |
    v
Save as Draft
    |
    v
Review Invoice
    |
    v
Finalize Invoice
    |
    v
Assign Invoice Number
    |
    v
Commit Invoice and Stock Changes Atomically
    |
    v
Invoice Details
    |
    +---- Record Payment
    |
    +---- Print / Download PDF
    |
    +---- Share Invoice
    |
    +---- Create Another Invoice
```

### 6.2 Invoice Form

The invoice form should include:

- Customer selection
- Customer creation shortcut
- Product search
- Barcode input or scanner support, where available
- Product quantity
- Unit price
- Discount
- Tax treatment
- Line-item total
- Subtotal
- Invoice-level discount, if supported
- Tax breakdown
- Final payable amount
- Notes and payment terms

The user should see the total update immediately when editable values change.

### 6.3 Invoice Validation

Before finalization, validate:

- Customer and business context
- Product and quantity details
- Valid prices and discounts
- Applicable tax configuration
- Stock availability, according to the configured stock policy
- Invoice numbering
- Required business and invoice fields

Do not allow negative quantities, invalid monetary values, or unauthorized price changes.

### 6.4 Finalization Rules

- A draft invoice can be edited or deleted according to permissions and policy.
- Finalization must be atomic and protected against duplicate submissions.
- Invoice number allocation must be concurrency-safe.
- Stock deduction and invoice finalization must succeed together or fail together.
- Finalized invoices must not be silently edited or deleted.
- Corrections should use supported cancellation, credit-note, debit-note, or other legally appropriate workflows.
- The original invoice and its audit history must remain traceable.

### 6.5 Invoice Statuses

- Draft
- Finalized
- Partially Paid
- Paid
- Overdue, where applicable
- Cancelled or Voided, according to the approved accounting workflow

Payment status should be derived from recorded payments, adjustments, due dates, and outstanding amounts rather than manually edited without reconciliation.

---

## 7. Payment Collection Flow

### Record Payment

```text
Invoice Details
      |
      v
Record Payment
      |
      v
Enter Amount and Payment Method
      |
      v
Enter Date and Reference (Optional)
      |
      v
Validate Amount
      |
      v
Save Payment
      |
      v
Update Invoice Balance
      |
      v
Payment Receipt / Confirmation
```

### Supported payment methods

- Cash
- UPI
- Bank transfer
- Card
- Other configurable methods

Recording a payment does not mean the application has processed a digital payment. Actual payment-gateway integration is a separate capability.

### Payment rules

- Support partial payments.
- Prevent duplicate payment records on retries.
- Do not accept an amount greater than the outstanding balance unless an explicitly supported advance or credit workflow permits it.
- Preserve payment history.
- Use reversals or adjustments rather than silently deleting reconciled payments.
- Keep payment records and invoice balances consistent.

### Customer outstanding flow

```text
Customers
    |
    v
Select Customer
    |
    v
View Outstanding Invoices
    |
    v
Open Invoice
    |
    v
Record Payment / Review History
```

---

## 8. Product and Inventory Flow

### 8.1 Add Product

```text
Inventory
   |
   v
Add Product
   |
   v
Enter Product Details
   |
   v
Set Price, Unit and Tax Configuration
   |
   v
Set Opening Stock (Optional)
   |
   v
Validate
   |
   v
Save Product
   |
   v
Product Details
```

### 8.2 Product List

The product list should support:

- Search by name, SKU, or barcode
- Category filtering
- Active or archived filtering
- Low-stock filtering
- Stock quantity sorting
- Price sorting
- Product detail access
- Bulk import, where supported

### 8.3 Stock Adjustment

```text
Inventory
   |
   v
Select Product
   |
   v
Adjust Stock
   |
   v
Choose Reason
   |
   v
Enter Quantity and Notes
   |
   v
Review Adjustment
   |
   v
Confirm
   |
   v
Create Stock Ledger Entry
   |
   v
Update Available Stock
```

Adjustment reasons may include:

- Damaged goods
- Expired goods
- Physical stock correction
- Opening stock
- Internal use
- Other authorized reasons

Every stock adjustment must capture the actor, timestamp, reason, and resulting movement.

### 8.4 Stock Movement Types

- Opening stock
- Sale
- Customer return
- Purchase receipt
- Supplier return
- Manual adjustment
- Transfer between branches, if enabled

Stock should be traceable through an append-only movement ledger. Current quantity should be derived from or reconciled against these movements.

### 8.5 Low-Stock Flow

```text
Dashboard
    |
    v
Low-Stock Alert
    |
    v
Filtered Product List
    |
    v
Select Product
    |
    v
Review Current Stock
    |
    v
Adjust Stock or Start Purchase
```

---

## 9. Customer Management Flow

### Add Customer

1. Open Customers.
2. Select Add Customer.
3. Enter customer name.
4. Add phone number and email if available.
5. Add billing address and GSTIN when applicable.
6. Save customer.
7. Open customer profile.

### Customer profile

Display:

- Contact information
- Relevant tax details
- Invoice history
- Total invoiced
- Payments received
- Outstanding balance
- Credit or adjustment history, where supported

### Customer actions

- Create invoice
- Record payment
- View invoices
- Edit contact details
- Archive customer

Customer records with financial history should not be hard-deleted if doing so would break invoice or audit references.

---

## 10. Supplier and Purchase Flow

This is a planned module that can be introduced after the core billing and inventory workflows are reliable.

### Add Supplier

- Enter supplier details.
- Add business address and GSTIN, if applicable.
- Save supplier.
- Open supplier profile.

### Record Purchase

```text
Suppliers & Purchases
        |
        v
Create Purchase
        |
        v
Select Supplier
        |
        v
Add Products and Quantities
        |
        v
Enter Purchase Prices and Taxes
        |
        v
Review Purchase
        |
        v
Confirm Goods Received
        |
        v
Record Stock Increase
        |
        v
Update Supplier Payable (If Tracked)
```

### Purchase rules

- Distinguish a purchase order from received goods.
- Increase stock when goods are actually received, not merely when an order is drafted.
- Track supplier payments separately from customer receipts.
- Record purchase returns as traceable transactions.
- Apply tax treatment according to the configured transaction and applicable rules.

---

## 11. Reports and Analytics Flow

### Reports home

Available report categories should include:

**Sales**

- Sales by day, week, or month
- Sales by product
- Sales by customer
- Invoice summaries

**Inventory**

- Current stock
- Low-stock report
- Stock movement history
- Inventory adjustments

**Receivables**

- Outstanding invoices
- Overdue balances
- Customer payment history

**Purchases**

- Purchase summaries
- Supplier balances, if enabled

### Report journey

```text
Reports
   |
   v
Select Report Type
   |
   v
Choose Date Range
   |
   v
Apply Filters
   |
   v
View Results
   |
   +---- Export CSV/PDF, where supported
   |
   +---- Open Related Record
```

Reports should respect user permissions and branch filters. Financial totals must have clear definitions and consistent treatment of discounts, taxes, returns, cancellations, and payments.

---

## 12. Staff and Role Management Flow

### Invite Staff

```text
Settings / Staff
       |
       v
Invite Staff Member
       |
       v
Enter Contact Details
       |
       v
Assign Role
       |
       v
Send Invitation
       |
       v
Staff Accepts Invitation
       |
       v
Account Joins Business
       |
       v
Access Limited by Permissions
```

### Initial roles

**Owner**

- Full business administration
- Subscription management
- Business configuration
- Staff and branch management

**Admin**

- Manage daily business operations
- Manage products, invoices, customers, and reports according to assigned permissions

**Manager**

- Oversee operations
- Review reports
- Approve restricted actions where configured

**Cashier**

- Create invoices
- Record payments
- View permitted customer information

**Inventory Staff**

- View products
- Perform permitted stock operations
- Access stock movement history

These are initial role templates. Permission checks must be enforced on the server, not just by hiding UI elements.

### Staff access rules

- Each user must belong to an authorized business membership.
- Branch restrictions must be enforced for branch-limited users.
- Revoked users must lose access promptly.
- Sensitive actions should be logged.
- Staff must not gain owner-level permissions by changing client-side state or requests.

---

## 13. Multi-Branch Flow

This module may be enabled by subscription plan or business configuration.

```text
Business Selector
       |
       v
Select Business
       |
       v
Select Branch
       |
       v
Load Branch-Scoped Dashboard
       |
       +---- Branch Inventory
       |
       +---- Branch Invoices
       |
       +---- Branch Customers
       |
       +---- Branch Reports
```

### Branch setup

- Create branch.
- Enter branch name and address.
- Configure permitted invoice and tax details.
- Assign staff.
- Define stock and invoice-numbering policies.
- Activate branch.

### Branch transfers

Where enabled:

1. Select source and destination branches.
2. Select products and quantities.
3. Create transfer record.
4. Record dispatch.
5. Record receipt at the destination.
6. Reconcile discrepancies.

A transfer must not create stock out of nothing or duplicate quantities. In-transit stock should be represented explicitly if the workflow requires it.

---

## 14. Subscription and Upgrade Flow

### Subscription entry points

- During onboarding
- Settings → Subscription
- Feature limit reached
- Premium feature selection
- Trial-expiry reminder

### Subscription journey

```text
Subscription Page
       |
       v
View Available Plans
       |
       v
Compare Features and Limits
       |
       v
Select Plan
       |
       v
Review Price and Billing Terms
       |
       v
Confirm Upgrade / Start Trial
       |
       v
Activate Entitlements
       |
       v
Subscription Dashboard
```

### Subscription capabilities

- Free plan
- Premium trial, subject to eligibility
- Paid plans based on validated customer needs
- Usage and feature limits
- Upgrade and downgrade
- Renewal and expiry status
- Billing history
- Cancellation and plan-change handling

Exact prices, limits, trial duration, and payment provider are pending business validation.

### Plan enforcement rules

- Enforce limits on the backend.
- Show a clear explanation when a limit is reached.
- Offer an upgrade path without blocking unrelated functions unnecessarily.
- Define what happens to existing data after downgrade or expiry.
- Never delete customer business data solely because a subscription expires.
- Do not enable paid entitlements until payment or trial eligibility is confirmed by the trusted subscription workflow.

---

## 15. Settings Flow

### Business settings

- Business profile
- GST and tax configuration
- Invoice preferences
- Branch configuration
- Language and regional preferences

### User settings

- Profile
- Password and security
- Active sessions, where supported
- Notification preferences

### Operational settings

- Product units and categories
- Payment methods
- Staff roles and permissions
- Import/export
- Subscription management
- Audit history

Critical settings should require suitable permissions and confirmation before changes are saved.

Changes to tax or invoice configuration must not silently alter already-finalized financial documents.

---

## 16. Search and Global Actions

The web app should provide a global search or quick-action menu.

Users may search for:

- Products
- Customers
- Invoices
- Suppliers
- Stock movements, when permitted

Quick actions may include:

- Create invoice
- Add product
- Add customer
- Record payment
- Adjust stock

Search results must be limited to the user's authorized business and branch scope.

---

## 17. Notifications and Alerts

### In-app alerts

- Low stock
- Overdue invoices
- Successful invoice finalization
- Payment recorded
- Import completed or failed
- Staff invitation status
- Subscription reminders

### Notification rules

- Avoid duplicate alerts.
- Allow configurable notification preferences.
- Do not include sensitive financial or customer information in notification previews unnecessarily.
- Distinguish an informational alert from a failed transaction.
- Provide a direct link to the related authorized record.

Email, SMS, WhatsApp, and push notifications should be treated as separate integrations and prioritized according to cost and customer validation.

---

## 18. Android-Specific Flow

### Home screen

Show:

- Today's sales
- Outstanding payments
- Low-stock count
- Recent activity

Primary actions:

- New bill
- Add product
- Find customer
- Record payment

### Mobile billing

```text
Home
 |
 v
New Bill
 |
 v
Search / Scan Product
 |
 v
Set Quantity
 |
 v
Add More Items
 |
 v
Select Customer
 |
 v
Review Total
 |
 v
Save Draft / Finalize
 |
 v
Record Payment
 |
 v
View or Share Invoice
```

### Mobile usability requirements

- Large touch targets
- Clear numeric input
- Fast product search
- Camera permission requested only when needed for scanning
- Keyboard-friendly billing forms
- Recoverable errors
- Clear loading and saving states
- Safe handling of interrupted requests

### Offline behavior

Offline invoice creation and synchronization should not be assumed in the initial MVP.

If offline support is introduced later, the design must account for duplicate submissions, stock conflicts, invoice-number allocation, permissions, and synchronization failures. Final invoice numbers must remain authoritative and unique after synchronization.

---

## 19. Common Error and Recovery Flows

### Network failure

- Preserve unsaved form data when safely possible.
- Display a clear connection error.
- Offer retry.
- Prevent duplicate finalization when the original request may have succeeded.

### Insufficient stock

- Show the affected product and available quantity.
- Allow the user to revise quantities.
- Allow an authorized override only if the business policy permits it.
- Do not silently create negative stock.

### Concurrent stock changes

- Revalidate stock during finalization.
- Use database transactions and appropriate locking or concurrency controls.
- Return a recoverable error if the requested quantity is no longer available.

### Duplicate submission

- Use idempotency protection for financial and stock-changing operations.
- Return the original transaction result when the same operation is retried safely.

### Import failure

- Validate the file before importing.
- Show row-level errors.
- Clearly report successful and unsuccessful rows.
- Prevent accidental duplicate imports where practical.

### Permission denied

- Explain that the user lacks permission.
- Provide a route to contact the business administrator.
- Do not expose protected record details.

---

## 20. Global Application Rules

1. Every business-owned record must be scoped to the correct business.
2. Branch access must be checked wherever branch restrictions apply.
3. All authorization checks must be enforced server-side.
4. Money must use precise decimal or integer-minor-unit representations, not binary floating-point arithmetic.
5. Invoice totals and tax calculations must be deterministic and tested.
6. Stock-changing operations must be transactional and auditable.
7. Finalized financial records must retain their history.
8. Payment balances must be reconcilable with the underlying transactions.
9. Important mutations must be safe to retry.
10. Subscription limits must be checked on the backend.
11. Dates, time zones, currency, and tax treatment must be explicit.
12. Sensitive data must be protected through appropriate access controls.
13. Destructive actions must include confirmation and suitable audit logging.
14. The interface must communicate success only after the server confirms it.

---

## 21. Recommended MVP Development Order

### Phase 1 — Foundation

- Authentication
- Business creation and membership
- Basic business profile
- Database authorization and tenant isolation
- Main navigation and design system

### Phase 2 — Products and Inventory

- Product CRUD
- Categories and units
- Opening stock
- Stock ledger
- Stock adjustments
- Low-stock alerts

### Phase 3 — Customers and Billing

- Customer CRUD
- Draft invoices
- Tax and total calculation
- Invoice finalization
- Stock deduction
- Invoice print/PDF

### Phase 4 — Payments

- Payment recording
- Partial payments
- Outstanding balances
- Payment history
- Receivables view

### Phase 5 — Dashboard and Reports

- Sales summaries
- Inventory reports
- Outstanding reports
- Recent activity

### Phase 6 — Android Core Workflows

- Login and business selection
- Dashboard
- Product lookup
- Billing
- Customer lookup
- Payment recording

### Phase 7 — Access and Monetization

- Staff roles
- Permission management
- Subscription entitlements
- Free plan and trial
- Upgrade experience

### Phase 8 — Expansion

- Suppliers and purchases
- CSV import/export
- Multi-branch operations
- Advanced reports
- Notifications and integrations

Prioritize security, financial correctness, and transaction integrity over adding many modules quickly.

---

## 22. MVP Acceptance Criteria

The first release is ready for controlled testing when:

- A user can create an account and set up a business.
- Authorized users can add and search products.
- Stock changes are traceable.
- A user can create and finalize an invoice.
- Invoice totals and applicable taxes are calculated correctly.
- Finalization and stock deduction cannot partially succeed.
- A user can record full or partial payments.
- Outstanding balances remain consistent with payment history.
- Users can print or download a finalized invoice.
- Dashboard and reports reflect the correct business data.
- Unauthorized users cannot access another business's records.
- Staff permissions are enforced on the backend.
- Repeated requests cannot create duplicate invoices, payments, or stock movements.
- Core workflows are usable on supported Android devices.
- Backup, recovery, monitoring, and error handling are tested before production launch.

---

## 23. Decisions Still Pending

- Final brand name and domain
- Exact free and paid plan limits
- Premium trial duration
- Invoice numbering policy per business or branch
- Supported inventory units and product variants
- Negative-stock policy
- Return, refund, cancellation, and credit-note workflows
- Whether purchases and suppliers belong in the first public release
- Whether customer and product imports are MVP requirements
- Offline support requirements
- Notification channels
- Payment provider and subscription billing method
- Required accounting and GST compliance review
- Launch region and initial pilot-business segment

These decisions should be finalized before the relevant modules are implemented.

---

**End of AppFlow.md**
