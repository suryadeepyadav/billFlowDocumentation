# SYV BillFlow End-User Documentation

This folder is the complete user manual for SYV BillFlow. It explains what each module does, what every form field means, which fields are required, how records move through their statuses, and how one module affects another.

The manual describes the application as it currently works. A menu, tab, button, or action may be hidden when it is not included in the tenant's subscription package or when the signed-in user does not have the required permission.

## Recommended Reading Order

New administrators should read the guides in this order:

1. [Getting Started](01-getting-started.md)
2. [Navigation, Tables, and Common Actions](02-navigation-tables-and-common-actions.md)
3. [Company, Tax, Financial Year, and Other Settings](03-company-tax-and-financial-settings.md)
4. [Business Masters](04-business-masters.md)
5. [Items and Inventory](05-items-and-inventory.md)
6. [Users, Permissions, and Subscription](13-users-permissions-and-subscription.md)
7. The transaction and workforce guides relevant to the business

Day-to-day users can begin with [End-to-End Workflows](15-end-to-end-workflows.md) and follow the links to the module they need.

## Documentation Map

| Guide | What it covers |
| --- | --- |
| [01 - Getting Started](01-getting-started.md) | Login, workspace access, first-time setup, and a safe setup order |
| [02 - Navigation, Tables, and Common Actions](02-navigation-tables-and-common-actions.md) | Sidebar, search, filters, sorting, columns, pagination, mobile actions, print, and Excel |
| [03 - Company, Tax, Financial Year, and Other Settings](03-company-tax-and-financial-settings.md) | Company profile, logo, GST, tax calculation, financial years, sequences, audit, and appearance |
| [04 - Business Masters](04-business-masters.md) | Customers, suppliers, categories, units, expense heads, and payment methods |
| [05 - Items and Inventory](05-items-and-inventory.md) | Items/services, stock summary, movement history, stock adjustments, and stock effects |
| [06 - Quotations](06-quotations.md) | Quotation fields, statuses, acceptance, cancellation, site creation, and invoice conversion |
| [07 - Invoices and Receipts](07-invoices-and-receipts.md) | Sales invoices, payment statuses, receipts, allocations, advances, cancellation, and outstanding |
| [08 - Purchases and Payments](08-purchases-and-payments.md) | Purchases, supplier payments, allocations, supplier advances, stock receipt, and cancellation |
| [09 - Site Management](09-site-management.md) | Sites, cash ledger, transfers, expenses, materials, work history, attachments, and costing |
| [10 - Employees and Compensation](10-employees-and-compensation.md) | Employees/workers, work locations, shifts, daily wage, monthly salary, and overtime setup |
| [11 - Attendance](11-attendance.md) | Daily entry, attendance statuses, check-in/out, overtime, submission, approval, locking, and reports |
| [12 - Payroll](12-payroll.md) | Payroll settings, runs, calculations, adjustments, advances, salary payments, reports, and payslips |
| [13 - Users, Permissions, and Subscription](13-users-permissions-and-subscription.md) | User accounts, roles, permission actions, feature licensing, limits, and access problems |
| [14 - Dashboard, Reports, Printing, and Exports](14-dashboard-reports-printing-and-exports.md) | Dashboard KPIs/charts, alerts, reports, CSV, Excel, print, PDF, and document output |
| [15 - End-to-End Workflows](15-end-to-end-workflows.md) | Practical sales, purchasing, site, inventory, attendance, payroll, and month-end workflows |
| [16 - Status Reference](16-status-reference.md) | Meaning and allowed next action for every major status |
| [17 - Glossary](17-glossary.md) | Plain-language definitions of accounting, GST, inventory, site, workforce, and system terms |
| [18 - Troubleshooting and FAQ](18-troubleshooting-and-faq.md) | Common user problems, causes, checks, and safe corrections |
| [19 - Customer and Supplier Statements](19-customer-and-supplier-statements.md) | Live balances, financial dashboards, date-range statements, ledgers, history, print, and CSV export |

## How Field Requirements Are Written

Each form guide uses one of these requirement labels:

- **Required**: The record cannot be saved without a valid value.
- **Optional**: The record can be saved without it.
- **Conditional**: It is required only for a particular status, document type, or workflow.
- **Calculated**: BillFlow derives the value; the user does not enter it directly.
- **Generated**: BillFlow assigns the value from a numbering sequence.

An optional field can still be important. For example, a customer state code is optional when saving the customer, but it is necessary for accurate CGST/SGST versus IGST selection.

## Important Safety Principle

BillFlow keeps business history by using statuses and reversal entries. Posted invoices, purchases, payments, receipts, site expenses, stock movements, and payroll records are not treated like disposable draft data. When a correction is required, use the available **Cancel**, **Reopen**, or reversal action instead of trying to remove the history.

## Product and Access Scope

BillFlow is tenant-based:

- Each company operates in its own workspace.
- Subscription features come from SYV Cloud.
- User permissions control what each person can list, create, view, update, approve, cancel, print, or export.
- The sidebar only shows modules available to both the tenant and the current user.
- Workforce work locations are currently independent from Site Management. They can be linked in a future version, but choosing a work location does not currently update a BillFlow site.

For a quick status lookup, keep [Status Reference](16-status-reference.md) open while learning the application.
