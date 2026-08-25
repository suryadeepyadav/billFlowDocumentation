# Dashboard, Reports, Printing, and Exports

# Dashboard

## What Is the Dashboard?

The Dashboard is a role-aware operating summary. It combines relevant financial, sales, purchasing, inventory, site, and workforce indicators according to the tenant's licensed features and the signed-in user's permissions.

It is designed to answer:

- What happened in the selected period?
- What money is outstanding?
- Which items need attention now?
- Which recent transactions should be reviewed?
- Where should the user continue working?

The Dashboard is not a replacement for detailed accounting reports. Use Reports and source documents to verify decisions.

## Period Selector

| Option | Period used |
| --- | --- |
| This month | Current calendar month |
| This quarter | Current calendar quarter |
| Financial year | Active/current configured financial-year context |
| Custom dates | User-entered From and To dates |

For Custom dates, both dates are required and From cannot be after To. Refresh reloads all visible summaries for the selected period.

Where a card shows a percentage change, it compares the selected period with the immediately preceding comparable period.

## Quick Actions

Quick Actions can include:

- New quotation
- New invoice
- Record receipt
- New purchase
- Record payment

An action appears only when its subscription feature is enabled and the user has Insert permission. The shortcut opens the same creation workflow used by its module.

## KPI Cards

BillFlow shows up to six of the most relevant available KPIs. The exact cards vary by entitlement and permission.

| KPI | Meaning |
| --- | --- |
| Sales revenue | Taxable value of Posted invoices in the selected period, excluding GST |
| Project profit | Site revenue less site material, direct purchase, and site expense cost for the period |
| Receivables | Current open customer invoice balances; overdue detail is highlighted |
| Payables | Current open supplier purchase balances; overdue detail is highlighted |
| Collections | Posted Receipt amounts in the selected period |
| Active sites | Count of active Sites |
| Site cash | Current operational cash balance across active Sites |
| Purchase value | Taxable value of Posted purchases in the selected period |
| Supplier payments | Posted supplier Payment amounts in the selected period |
| Quoted value | Value/count of active quotations for the selected period |
| Accepted value | Value/count of Accepted quotations |
| Acceptance rate | Accepted quotations versus decided quotation outcomes |
| Awaiting response | Sent quotations waiting for customer response |
| Draft quotations | Quotations still being prepared |
| Stock items | Count of active Stock-type items |
| Stock alerts | Low-stock and out-of-stock item count |
| Active workforce | Active employee/worker count |
| Today attendance | Present and total attendance records for today |
| Salary outstanding | Unpaid balance across open Posted payroll entries/runs |

Click a card to open its source module. Compact currency values may be abbreviated on the card; the full formatted value is available in the card context/tooltip.

## Performance Trend

The trend chart adapts to available modules:

- **Project performance**: Site revenue excluding GST, project cost, and profit/loss by month.
- **Sales and purchasing**: Posted taxable sales and purchase value by month.
- **Quotation momentum**: Quoted value by month when quotation data is the main available capability.

Use the trend to spot direction and unusual periods. Open Reports before concluding why a value changed.

## Needs Attention

The attention list prioritizes current operational exceptions and links to the relevant module. Possible alerts include:

- Overdue invoices
- Overdue purchases
- Unallocated customer receipts
- Unallocated supplier payments
- Quotations expiring within seven days
- Quotation drafts older than fourteen days
- Out-of-stock items
- Low-stock items
- Pending attendance approval
- Payroll runs needing action
- Negative Site cash
- Loss-making Sites for the selected period

The list shows a limited set of highest-priority alerts. Absence of an alert does not replace routine reconciliation.

## Outstanding Aging

The aging chart separates Receivables and/or Payables into:

- Current
- 1-30 days overdue
- 31-60 days overdue
- 61-90 days overdue
- More than 90 days overdue

Aging is based on outstanding document balance and due date. A missing or incorrect due date can make the analysis misleading.

## Site Profitability

Where Site access is available, the chart compares selected Site profit/loss values. Positive and loss-making sites are visually distinguished.

Revenue and cost definitions follow [Site Management](09-site-management.md). Contract value is commercial context and is not automatically recognized as revenue.

## Quotation Pipeline

The quotation chart summarizes counts by status, such as Draft, Sent, Accepted, Rejected, and Cancelled, for the selected period. Use it to identify delayed follow-up or conversion performance.

## Recent Transactions

Recent activity can include permitted Quotations, Invoices, Receipts, Purchases, Payments, Site Expenses, and workforce transactions. Each row provides a quick link to the source area.

Recent means recently created/updated activity, not a complete chronological audit log.

## Mobile Use

On smaller screens:

- Period controls wrap into a compact layout.
- Quick Actions scroll horizontally.
- KPI cards and panels stack vertically.
- Charts retain a fixed usable height and support touch tooltips.
- Detailed investigation should continue in responsive lists/reports.

For a clean mobile view, use the Dashboard for exceptions and navigation, then open the specific module for full details.

# Reports

## What Is the Reports Module?

Reports provides server-side, tenant-scoped business views. It supports shared search, filters, multi-sort, pagination, table printing/Excel, and a complete filtered CSV download.

## Report Catalog

### Site P&L

Shows:

- Site, Customer, and status
- Contract value
- Invoiced total
- Tax-excluded revenue
- Customer outstanding
- Material cost
- Direct purchase cost
- Site expense cost
- Total cost
- Profit/loss and margin
- Current Site cash

Use a date range to analyze performance for a period.

### Site Cash Flow

Shows Customer receipts, company fund transfers, supplier payments, Site expenses, and current Site cash by Site.

Customer Receipts and supplier Payments are shown as broader cash-flow context. They do not themselves change the operational Site Ledger balance; Fund Transfers and Site Expenses do. See [Site Management](09-site-management.md).

### Sales

Shows Invoice number/date, Customer, Site, taxable value, tax, total, balance, payment status, and document status.

### Purchases

Shows Purchase number/date, supplier invoice, Supplier, Site, taxable value, tax, total, balance, payment status, and document status.

### Receipts

Shows Receipt number/date, Customer, Site, amount, allocated amount, unallocated advance, reference, and status.

### Payments

Shows Payment number/date, Supplier, Site, amount, allocated amount, unallocated advance, reference, and status.

### Customer Outstanding

Shows Customer, invoiced amount, received amount, opening balance, Customer advance, and current outstanding. It uses all posted receipt amounts, including unallocated Customer advances. This is a current-balance report and has no report date range.

### Supplier Outstanding

Shows Supplier, purchased amount, paid amount, opening balance, advance amount, and current outstanding. This is a current-balance report and has no report date range.

For one party's Financial Year/date-range balance, document history, and debit/credit ledger, use the Customer or Supplier dashboard from the master list. See [Customer and Supplier Statements](19-customer-and-supplier-statements.md).

### Stock

Shows Item code/name, minimum stock, Warehouse quantity, quantity at Sites, total quantity, and low-stock indicator. This is a current-stock report and has no date range.

### Site Expenses

Shows expense number/date, Site, Expense Head, Vendor, bill number, amount, and status.

### Site Materials

Shows material transaction/date, Site, issue/return type, Items, total quantity, value, and status.

### Site Ledger

Shows date, Site, entry type, direction, amount, running balance, reference, and narration.

### Stock Movements

Shows date, Item, location, movement type/direction, quantity, rate, value, reference, and narration.

## Date Range Behavior

Transaction and Site-period reports use From/To dates. Current-balance reports such as Customer Outstanding, Supplier Outstanding, and Stock intentionally ignore date range because they show the present state.

Always check the active report title and period before exporting.

## Search, Filter, Sort, and Paging

Reports use server-side operations:

- Search sends the term to the backend.
- Advanced filters are translated into report conditions.
- Sorting occurs on the backend.
- Paging loads only the requested page.

This keeps large datasets responsive. See [Navigation, Tables, and Common Actions](02-navigation-tables-and-common-actions.md).

# Printing and Exporting

## Table Print

The table Print action creates a printable view of the currently displayed/loaded rows and visible columns. It respects local column selection and current table state.

Use it for a short operational list, not as evidence that every matching server row was printed.

## Table Excel

The shared table Excel action exports the currently displayed/loaded rows and selected columns. On a server-paged list, this normally means the current page.

## Download Full CSV Report

The Reports download icon requests the complete report using the current server-side report filters and sort, rather than only the visible page. Use this option for full reconciliations, archiving, or analysis in spreadsheet software.

Before download:

1. Select the correct report.
2. Set From/To where applicable.
3. Apply Search, Filters, and Sort.
4. Review a sample page.
5. Select **Download full CSV report**.

The user needs Reports Export permission.

## Document Printing

Quotation, Invoice, Purchase, Receipt, and related print actions open a dedicated printable document. Prints use:

- Company profile and uploaded logo
- Party/document details
- Line items and totals
- Applicable terms/notes
- Only non-zero optional tax/discount rows

CGST, SGST, IGST, Discount, and other optional total lines are hidden when they are zero, keeping documents clean.

Document lifecycle remains visible on printed copies:

- **Draft**: `DRAFT` watermark, status in the title, and a document-specific disclaimer explaining that no posting, allocation, balance, or stock effect exists.
- **Posted/active**: Clean business-document layout without a lifecycle watermark.
- **Cancelled**: `CANCELLED` watermark and reference-only disclaimer.

Draft Receipt output specifically says it is not proof of payment. Printing does not post a document or change any business data.

Browser pop-up blocking can prevent the print window from opening. Allow pop-ups for the BillFlow domain and try again.

## Print Review Checklist

- Company name, address, GSTIN, and logo are correct.
- Customer/Supplier details are correct.
- Document number and date are correct.
- GST type and amount match the party state.
- Item quantities, rates, and discount are correct.
- Terms, notes, due/validity dates are appropriate.
- Cancelled documents are not sent as active documents.

## Permission Reference

| Action | Typical permission |
| --- | --- |
| Open Dashboard | Dashboard View |
| Refresh Dashboard | Dashboard View |
| Open Reports | Reports View/List |
| Print table/report/document | Module Print |
| Export visible table | Module Export |
| Download full report CSV | Reports Export |

Feature entitlements still apply. A user sees only charts, KPIs, quick actions, and reports supported by licensed and permitted modules.

## Common Mistakes

- Treating Dashboard cards as a full ledger or audited statement.
- Comparing taxable revenue with GST-inclusive cash without understanding the basis.
- Assuming Contract value equals Site revenue.
- Ignoring unallocated receipts/payments.
- Exporting the visible page when a full report was intended.
- Using a date range on a current-balance report and expecting historical balances.
- Forgetting that table column choices affect table print/Excel.
- Blocking the document print pop-up.
- Distributing a print before checking company/GST settings.

Continue with [End-to-End Workflows](15-end-to-end-workflows.md).
