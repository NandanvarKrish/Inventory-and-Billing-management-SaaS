
# UI/UX Design Brief
## Billing & Inventory SaaS

**Version:** 1.0  
**Status:** Draft  
**Platforms:** Web SaaS + Android  
**Target Market:** India  
**Related Documents:** `PRD.md`, `TRD.md`

---

## 1. Design Vision

Create a premium, modern, warm, and approachable business management application that Indian business owners can comfortably use throughout the working day.

The product must feel more thoughtful than a conventional accounting dashboard or generic admin template. Its interface should combine the clarity of modern productivity software with the reliability expected from financial and inventory tools.

### Design Goals

- Make everyday billing and inventory operations effortless.
- Reduce cognitive load and unnecessary navigation.
- Present financial information clearly and accurately.
- Make important actions easy to discover.
- Support both non-technical shop owners and experienced business operators.
- Maintain a consistent experience across web and Android.
- Create a distinctive visual identity using the approved earthy color palette.
- Balance aesthetic quality with operational efficiency.

**Core design principle:** Beautiful enough to stand out, practical enough to use every day.

---

## 2. Target Users

### Primary Users

- Small shop owners.
- Retailers and wholesalers.
- Business managers.
- Cashiers and billing operators.
- Inventory operators.
- Accountants and report viewers.

### User Characteristics

The interface must account for users who:

- May not be technically experienced.
- Perform repetitive tasks under time pressure.
- Need accurate information at a glance.
- Work with large product catalogues and invoice lists.
- May use older or smaller Android devices.
- Prefer straightforward terminology over technical jargon.
- Need reliable access to business information during busy hours.

---

## 3. Brand Personality

The interface should communicate the following qualities.

| Quality | Design interpretation |
|---|---|
| Trustworthy | Consistent layouts, clear totals, predictable actions |
| Premium | Refined typography, thoughtful spacing, precise alignment |
| Warm | Earthy colors and soft neutral backgrounds |
| Modern | Clean components, responsive layouts, subtle motion |
| Efficient | Short workflows, keyboard support, useful shortcuts |
| Approachable | Clear labels, friendly empty states, helpful feedback |
| Professional | Structured tables, readable numbers, restrained decoration |

Avoid making the application look rustic, overly decorative, childish, or excessively corporate.

---

## 4. Official Color Palette

Use the following colors as the foundation of the design system.

| Color Name | Hex | Primary Usage |
|---|---|---|
| Dark Walnut | `#582F0E` | Brand accents and selected primary actions |
| Saddle Brown | `#7F4F24` | Secondary brand emphasis |
| Toffee Brown | `#936639` | Supporting accents and selected elements |
| Camel | `#A68A64` | Muted decorative accents and supporting details |
| Khaki Beige | `#B6AD90` | Subtle borders and neutral accents |
| Dry Sage | `#C2C5AA` | Soft highlights and secondary surfaces |
| Dry Sage 2 | `#A4AC86` | Selected states and supporting accents |
| Dusty Olive | `#656D4A` | Navigation accents and secondary actions |
| Ebony | `#414833` | Strong text and dark interface elements |
| Charcoal Brown | `#333D29` | Main sidebar and brand-defining dark surfaces |

### 4.1 Supporting Neutrals

These are additional interface neutrals, not replacements for the official palette.

| Token | Hex | Usage |
|---|---|---|
| Warm Ivory | `#F7F5EE` | Main workspace background |
| Soft White | `#FFFFFF` | Cards, forms, dialogs |
| Pale Border | `#E7E3D8` | Dividers and subtle borders |
| Primary Text | `#292D24` | Main readable text |
| Secondary Text | `#6F7267` | Descriptions and secondary labels |

### 4.2 Color Distribution

Recommended starting balance:

- 60% warm ivory and light neutral surfaces.
- 25% white cards and content surfaces.
- 10% olive and sage tones.
- 5% brown brand accents.

These percentages are visual guidance, not rigid rules.

### 4.3 Usage Rules

- Use Charcoal Brown for the primary desktop sidebar.
- Use Dark Walnut sparingly for important primary actions.
- Use Dry Sage for subtle selection backgrounds.
- Use Dusty Olive for secondary navigation emphasis.
- Keep large content areas light.
- Avoid using all ten colors in a single screen.
- Use semantic colors for success, warning, error, and informational states.
- Never communicate status using color alone.
- Validate foreground/background contrast for all text and interactive states.

---

## 5. Typography System

Use three complementary typefaces.

### 5.1 Primary UI Font — DM Sans

Use for:

- Navigation.
- Forms and labels.
- Tables.
- Buttons.
- Descriptions.
- General interface text.

### 5.2 Display Font — Manrope

Use for:

- Page titles.
- Dashboard metrics.
- Section headings.
- Empty-state headings.
- Important business summaries.

### 5.3 Monospaced Font — IBM Plex Mono

Use selectively for:

- Invoice numbers.
- Product SKUs.
- Transaction identifiers.
- Structured reference codes.
- Numerical columns requiring alignment.

### 5.4 Type Scale

| Element | Suggested Size |
|---|---|
| Page title | 28–32 px |
| Section heading | 20–24 px |
| Card heading | 16–18 px |
| Body text | 14–16 px |
| Table text | 13–14 px |
| Helper text | 12–13 px |
| Primary dashboard metric | 28–36 px |

Use appropriate font weights and line heights. Avoid excessively small text, especially for invoice totals, product prices, and form labels.

Use tabular numerals for financial figures where supported.

---

## 6. Overall Application Layout

### 6.1 Desktop Web Layout

Use a persistent sidebar and a flexible main workspace.

```text
┌──────────────────────────────────────────────────────────────┐
│ Brand / Workspace       Search       Help     Profile        │
├───────────────┬──────────────────────────────────────────────┤
│               │                                              │
│ Dashboard     │ Page title                    Primary action │
│ Billing       │ Description / filters                        │
│ Inventory     │                                              │
│ Products      │ ┌──────────┐ ┌──────────┐ ┌──────────┐       │
│ Customers     │ │ Metric 1 │ │ Metric 2 │ │ Metric 3 │       │
│ Suppliers     │ └──────────┘ └──────────┘ └──────────┘       │
│ Reports       │                                              │
│ Team          │ Main content, tables, charts, and forms      │
│ Settings      │                                              │
│               │                                              │
├───────────────┴──────────────────────────────────────────────┤
│ Contextual help or status information where necessary        │
└──────────────────────────────────────────────────────────────┘
```

### 6.2 Layout Principles

- Sidebar width: approximately 230–260 px on desktop.
- Main content maximum width: adapt to the task and available space.
- Use a consistent spacing scale based on 4 px increments.
- Keep important actions in predictable positions.
- Use sticky table headers where useful.
- Allow dense operational tables to use horizontal scrolling only when necessary.
- Avoid excessive card nesting.
- Preserve sufficient whitespace without sacrificing information density.

### 6.3 Navigation

Recommended primary navigation:

1. Dashboard
2. Billing
3. Inventory
4. Products
5. Customers
6. Suppliers
7. Reports
8. Team
9. Settings

Navigation visibility must respect user permissions.

The final navigation structure can be adjusted after usability testing.

---

## 7. Dashboard Design

### Purpose

Help business owners understand the current state of their business within a few seconds.

### Layout

#### Header

- Greeting or business context.
- Current date or selected reporting period.
- Business/branch selector when applicable.
- Primary action: `Create Invoice`.

#### KPI Cards

- Today's Sales.
- Invoices Created.
- Outstanding Payments.
- Low-Stock Products.

#### Main Content

- Sales trend chart.
- Recent invoices.
- Low-stock product list.
- Outstanding customer balances.
- Recent inventory activity.

### Design Rules

- Keep the most actionable information near the top.
- Make metric labels explicit.
- Provide understandable date filters.
- Show comparison periods only when meaningful.
- Avoid charts that do not help users make decisions.
- Use concise tooltips for definitions.
- Provide helpful empty states for new businesses.
- Ensure dashboard figures reconcile with underlying transactions.

---

## 8. Billing and Invoice Creation

Billing is one of the most important workflows and should be optimized for speed.

### 8.1 Invoice List

Include:

- Invoice number.
- Customer.
- Invoice date.
- Total amount.
- Amount paid.
- Balance due.
- Status.
- Actions.

Support:

- Search.
- Date filtering.
- Status filtering.
- Customer filtering.
- Sorting.
- Pagination.
- Printable or downloadable invoice access.

### 8.2 Invoice Creation Screen

Recommended structure:

```text
┌─────────────────────────────────────────────────────────────┐
│ Create Invoice                              Save Draft       │
├─────────────────────────────────────────────────────────────┤
│ Customer                Invoice Number     Invoice Date     │
│ [Select customer]       [Generated]        [Date]           │
├─────────────────────────────────────────────────────────────┤
│ Add Products / Search SKU                                    │
├─────────────────────────────────────────────────────────────┤
│ Product       Qty       Price       Tax       Total          │
│ Product A     2         ₹500        ...       ...            │
│ Product B     1         ₹800        ...       ...            │
├─────────────────────────────────────────────────────────────┤
│ Notes / Payment Information                 Invoice Summary  │
│                                            Subtotal          │
│                                            Discount          │
│                                            Tax               │
│                                            Grand Total       │
├─────────────────────────────────────────────────────────────┤
│ Cancel                         Save Draft    Finalize Invoice│
└─────────────────────────────────────────────────────────────┘
```

### 8.3 Interaction Requirements

- Product search should be fast.
- Keyboard navigation should be supported on desktop.
- Quantity and price inputs should be easy to edit.
- Totals should update clearly as permitted values change.
- Validation errors should appear near relevant fields.
- Destructive actions require appropriate confirmation.
- Finalization should show a clear loading state and prevent accidental duplicate submissions.
- Failed requests must not create duplicate invoices or stock movements.
- Show success feedback and the resulting invoice number.
- Preserve a draft when safe and technically feasible.

### 8.4 Invoice Finalization

Before finalization:

- Validate required customer and invoice fields.
- Validate product quantities.
- Validate stock policy.
- Validate applicable tax calculations.
- Show the final total.
- Explain any blocking errors.

Finalization must be authorized and transaction-safe on the backend.

### 8.5 Invoice Preview

The printable invoice should be clean and professional.

Include the required business details, customer information, invoice identifier, line items, applicable taxes, totals, and payment details.

Use an appropriate print stylesheet and generate PDFs from authoritative finalized invoice data.

Tax-specific fields must be validated against applicable Indian requirements.

---

## 9. Inventory Management

### 9.1 Inventory Overview

Display:

- Product name.
- SKU.
- Category.
- Recorded stock.
- Unit.
- Stock value, if supported.
- Low-stock threshold.
- Stock status.
- Last movement.

### 9.2 Stock Status

Use clear text labels:

- In Stock.
- Low Stock.
- Out of Stock.
- Negative Stock, only if explicitly permitted.

Combine labels with appropriate icons or visual indicators.

### 9.3 Product Details

Provide:

- Product information.
- Current recorded quantity.
- Stock movement history.
- Price and tax details.
- Low-stock threshold.
- Authorized adjustment actions.

### 9.4 Stock Adjustment

The adjustment flow should request:

- Product.
- Branch, when applicable.
- Adjustment quantity.
- Adjustment reason.
- Confirmation.

After saving, show the updated quantity and movement history.

Never make stock appear to change without a traceable transaction.

---

## 10. Products, Customers, and Suppliers

### Product Management

- Simple creation and editing forms.
- Searchable product catalogue.
- Clear required-field indicators.
- SKU and pricing displayed prominently.
- Stock information accessible from product details.
- Archive instead of permanent deletion when historical records depend on a product.

### Customer Management

- Searchable customer list.
- Contact and billing details.
- Invoice history.
- Outstanding balance.
- Payment history.
- Clear customer creation flow.

### Supplier Management

- Supplier directory.
- Contact information.
- Purchase history when supported.
- Associated stock receipts where applicable.

Use consistent patterns across all list and detail pages.

---

## 11. Tables and Data Density

Business applications require information-dense interfaces, but dense does not mean cluttered.

### Requirements

- Clear column headings.
- Consistent numeric alignment.
- Tabular numerals for monetary amounts.
- Predictable row heights.
- Visible hover and focus states.
- Sticky headers where useful.
- Search, sorting, and filtering.
- Pagination for large datasets.
- Clear empty states.
- Accessible row actions.

Avoid using decorative charts, excessive badges, or oversized cards when a simple table communicates the information better.

---

## 12. Forms and Validation

### Form Principles

- Group related fields.
- Use explicit labels.
- Explain required fields.
- Use sensible defaults.
- Minimize unnecessary input.
- Preserve user input after recoverable failures.
- Clearly identify validation errors.
- Provide helpful examples for unfamiliar tax fields.

### Error Messages

Prefer:

- "Enter a valid quantity."
- "This invoice cannot be finalized because stock is insufficient."
- "You don't have permission to adjust inventory."
- "Your changes could not be saved. Please try again."

Avoid technical stack traces and vague messages such as "Something went wrong" when a more useful explanation is possible.

---

## 13. Empty, Loading, and Error States

Every major page must define the following states.

### Empty State

Explain what the page is for and provide one useful next action.

Example: "No products yet. Add your first product to start tracking stock."

### Loading State

Use restrained skeletons or progress indicators. Avoid flashing entire pages unnecessarily.

### Success State

Confirm the completed action and provide the next useful option.

### Error State

Explain the problem and provide a retry or recovery action where appropriate.

### Permission State

Explain that the current account does not have access and, where appropriate, direct the user to the business owner or administrator.

---

## 14. Android UX Requirements

The Android app should be designed specifically for smaller screens rather than being a scaled-down desktop interface.

### Navigation

Use an appropriate mobile navigation pattern with primary destinations easy to reach.

Potential primary destinations:

- Home.
- Billing.
- Inventory.
- Customers.
- More.

The exact navigation should be tested with target users.

### Mobile Interaction

- Touch targets should generally be at least 48 × 48 dp.
- Keep primary actions within comfortable reach.
- Use appropriate numeric keyboards for quantity and monetary inputs.
- Avoid unnecessarily long forms.
- Support clear loading and retry states.
- Prevent duplicate submissions.
- Handle expired sessions gracefully.
- Make invoice details readable on small screens.

### Offline Considerations

Do not imply that billing or inventory works offline until offline data storage, conflict handling, synchronization, and transaction rules have been implemented and tested.

---

## 15. Responsive Design

### Desktop

- Full sidebar.
- Multi-column dashboards.
- Wide operational tables.
- Keyboard-friendly workflows.
- Efficient invoice creation.

### Tablet

- Compact navigation.
- Flexible card layouts.
- Responsive forms.
- Table adaptation where practical.

### Mobile Web

- Collapsible navigation.
- Single-column forms.
- Simplified tables or stacked record views.
- Accessible action menus.

### Android

Use native mobile interaction patterns and touch-friendly controls.

Avoid simply shrinking desktop components to fit smaller displays.

---

## 16. Motion and Micro-Interactions

Animation should add clarity rather than distraction.

### Recommended

- Subtle button hover and press feedback.
- Short transitions between interface states.
- Smooth opening of menus and dialogs.
- Gentle chart entrance animations.
- Clear progress feedback for long-running actions.

### Avoid

- Excessive parallax.
- Large animated backgrounds.
- Constantly moving dashboard elements.
- Long transitions on repetitive tasks.
- Animation that delays saving or navigation.
- Decorative motion that interferes with data entry.

Respect reduced-motion preferences.

---

## 17. Iconography and Illustrations

Use Lucide icons consistently.

### Guidelines

- Use icons with text labels for important actions.
- Keep icon stroke weights consistent.
- Avoid mixing multiple icon styles.
- Use illustrations sparingly.
- Prefer simple, purposeful empty-state illustrations.
- Never rely on an icon alone when the action is unfamiliar or consequential.

Avoid excessive emoji use in the production interface.

---

## 18. Accessibility

Target WCAG 2.2 AA where applicable.

Requirements:

- Sufficient text and control contrast.
- Keyboard navigation.
- Visible focus indicators.
- Proper form labels.
- Semantic page structure.
- Accessible names for icon-only controls.
- Screen-reader-compatible validation messages.
- Non-color indicators for statuses.
- Reduced-motion support.
- Appropriate touch target sizes.

Test critical workflows with keyboard navigation and automated accessibility tools.

---

## 19. Design System and Component Library

Create reusable components for:

- Buttons.
- Inputs.
- Selects.
- Date pickers.
- Search fields.
- Data tables.
- Pagination.
- Cards.
- Dialogs.
- Drawers.
- Dropdown menus.
- Status indicators.
- Toast notifications.
- Tabs.
- Tooltips.
- Empty states.
- Loading skeletons.
- Page headers.
- Invoice line items.
- Financial summary panels.

### Component Rules

- Use consistent design tokens.
- Define default, hover, focus, active, disabled, loading, and error states.
- Maintain consistent spacing and border radii.
- Ensure accessible interaction patterns.
- Avoid creating duplicate components for the same purpose.
- Keep business logic separate from presentation where practical.

---

## 20. UX Performance Requirements

- Common actions should feel immediate under normal network conditions.
- Avoid unnecessary page reloads.
- Provide feedback for operations that take time.
- Paginate large datasets.
- Debounce search where appropriate.
- Avoid blocking the entire application for unrelated requests.
- Preserve form data after recoverable errors.
- Ensure UI totals remain consistent with authoritative server results.

Visual responsiveness must never compromise financial or inventory correctness.

---

## 21. Design Deliverables

The design process should produce:

1. User personas and key user journeys.
2. Information architecture.
3. Sitemap and navigation model.
4. Low-fidelity wireframes.
5. High-fidelity dashboard design.
6. Invoice creation and preview designs.
7. Inventory and product management designs.
8. Customer and supplier management designs.
9. Reports and settings designs.
10. Android navigation and key screens.
11. Design tokens and typography specifications.
12. Reusable component library.
13. Responsive layouts.
14. Interaction and validation states.
15. Accessibility review.
16. Usability testing results.

---

## 22. Usability Testing

Test the application with representative business owners and staff.

### Core Tasks

- Set up a business.
- Add a product.
- Enter opening stock.
- Create and finalize an invoice.
- Record a payment.
- Find a low-stock product.
- Review an outstanding customer balance.
- Find a previous invoice.
- Invite an employee and configure permissions.

### Measure

- Task completion rate.
- Time to complete common tasks.
- Number of errors.
- Number of steps required.
- User confidence.
- Areas where users request help.

Use findings to refine the interface before expanding the feature set.

---

## 23. Design Acceptance Criteria

The UI/UX is ready for implementation when:

- Primary navigation is finalized.
- Key web and Android user flows are documented.
- Invoice creation is optimized for speed and clarity.
- Inventory changes are clearly communicated.
- Financial information is easy to scan.
- The approved color palette is consistently applied.
- Typography is readable across screen sizes.
- Components have documented interaction states.
- Loading, empty, success, and error states are designed.
- Accessibility requirements are reviewed.
- Responsive behavior is specified.
- Critical workflows have been tested with representative users.

---

## 24. Final Design Direction

Build an interface that feels like a premium modern productivity application adapted for real business operations.

The visual identity should combine:

- Charcoal and olive navigation.
- Warm ivory workspaces.
- Sage-tinted supporting surfaces.
- Restrained walnut accents.
- DM Sans for everyday interface text.
- Manrope for headings and metrics.
- IBM Plex Mono for selected identifiers and numerical details.

Prioritize clarity, consistency, and comfort over decorative complexity.

**Final principle:** The application should feel calm when the business is busy, clear when the numbers matter, and effortless when the same task is repeated hundreds of times.
