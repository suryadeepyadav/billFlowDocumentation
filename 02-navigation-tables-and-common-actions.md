# Navigation, Tables, and Common Actions

## What Is Covered Here?

BillFlow uses the same navigation, table, filtering, action, confirmation, and print patterns across modules. Learning these controls once makes the rest of the application much easier to use.

## Sidebar Navigation

The sidebar is arranged by business area:

| Group | Typical modules |
| --- | --- |
| Sales | Customers, Quotations, Sales Invoices, Receipts |
| Purchasing | Suppliers, Purchases, Payments |
| Inventory | Stock Control, Items & Services, Units, Categories |
| Sites & Expenses | Sites, Expense Heads |
| Workforce | Employees & Workers, Attendance, Payroll |
| Administration | Reports, Payment Methods, Users & Permissions, Settings |

Select a group to expand or collapse it. **Home** and **Dashboard** are primary menu items outside the groups.

## Mobile Home and Bottom Navigation

On phones and compact tablets, BillFlow opens **Home** after sign-in instead of loading the analytical Dashboard. Desktop users continue to open Dashboard first.

Mobile Home contains every module available under the tenant subscription and the signed-in user's permissions. Features are arranged in compact cards under the same business groups used by the sidebar.

- Select a feature card to open its list or workspace.
- Select the plus icon on a card to open that module's primary creation form directly.
- Use **Find a feature** to filter the launcher by module, action, or common business term.
- **Quick access** shows recently opened modules. Before any history exists, it shows relevant daily-work modules available to the user.

The fixed mobile navigation bar provides:

| Action | Purpose |
| --- | --- |
| Home | Return to the feature launcher |
| Add | Open all permitted create actions, grouped by business area |
| Dashboard | Open financial and operational analytics when permitted |
| More | Open the complete sidebar navigation drawer |

The Add and Dashboard destinations are hidden when the user does not have the required access. Selecting a feature from More closes the drawer automatically. Long page names may be shortened in the top bar, but the page itself still shows its full title.

Home history is stored only in the current browser and is separated by tenant and user. It does not change permissions or subscription access.

## Why a Menu May Be Missing

A menu is visible only when all applicable checks pass:

- The tenant subscription includes the feature.
- Required dependent features are enabled. Attendance requires Employees and Attendance; Payroll requires Employees, Attendance, and Payroll.
- The current user has access to the module.

Site Work History is shown as a tab inside a site, not as a separate sidebar item.

## Page Header Actions

Most list pages use a compact header:

- The page title identifies the current module.
- A plus icon creates a new record.
- Other icon buttons represent a clear page-level action such as stock adjustment or refresh.
- Hover an icon to read its tooltip on devices that support hover.

A disabled icon means the action is not valid for the record or the user lacks permission.

Mobile Home and Quick Add use the same creation forms as the page-level plus icons. A direct creation shortcut never bypasses backend permission checks.

## Shared Data Table Toolbar

Most BillFlow lists use the shared Smart Data Table.

### Search

Type in the Search field to search the fields supported by that list. Search is delayed briefly while typing to avoid sending a request for every keystroke.

On large transaction lists, searching is server-side and returns a paged result. On small master lists that are already loaded, filtering can run locally in a background worker.

### Print

The printer icon opens a printable view of the visible table columns and currently displayed rows.

Important: for a server-paginated list, table Print uses the rows currently loaded on the page. It is not a full-database export. For complete report data, use the Reports module and its full CSV download.

### Export Excel

The Excel icon exports the visible columns and currently displayed rows to an Excel-compatible file.

As with table Print, a server-paginated screen exports the currently loaded page. Use **Reports > Download full CSV report** for a complete filtered report.

### Choose Columns

Use the columns icon to:

1. Select which columns are visible.
2. Keep at least one data column visible.
3. Select **Save** to remember the choice for that table.
4. Select **Reset** to restore the default columns.

Column preferences are stored for the current browser. The Actions column may remain fixed because it is required for row operations.

### Advanced Filter

Use the filter icon to build one or more conditions.

Each condition contains:

| Part | Purpose |
| --- | --- |
| Data/Field | The column to filter |
| Condition | The comparison, such as equals, contains, greater than, before, after, or between |
| Value | The text, number, boolean, or date to compare |

Use **AND** when every condition must match. Use **OR** when a row may match any condition.

Select **Apply** to activate the rules. A badge on the filter icon indicates active filters. Select **Clear** to remove all filter rules.

Available conditions depend on the field type. For example, a date can use date comparisons, a number can use range comparisons, and text can use contains/equality comparisons.

### Sorting Order

Use the sorting icon to create one or more sort levels:

1. Choose a column.
2. Choose ascending or descending order.
3. Select the plus icon to add it.
4. Add more columns if a secondary order is needed.
5. Select **Save** to apply the order.

Select **Reset** to return to the list's default sort.

### Date Range

Reports and some time-based lists show a date-range control. Choose a From and To date, then Apply. The end date must not be before the start date.

### Refresh

Use Refresh after another user has changed data, after a related transaction was posted, or when a newly created dropdown record is not yet visible.

### Pagination and Rows

At the bottom of a server-side table:

- **Showing X to Y of Z entries** describes the current result.
- **Rows** controls the number of records per page.
- Previous and Next buttons move through pages.

Changing search, filters, date range, or sort normally returns the list to page 1.

## Row Actions

Common row actions include:

| Icon/action | Meaning |
| --- | --- |
| View | Open a record preview or detail page |
| Edit | Change a record that is still editable |
| Print | Print the business document or save it as PDF through the browser |
| Accept/Approve | Confirm a controlled workflow transition |
| Create Site | Create a site from an accepted quotation |
| Create Invoice | Start an invoice from an accepted quotation |
| Outstanding | View open customer or supplier balances |
| Deactivate | Hide a master from new transactions without deleting history |
| Reactivate | Make an inactive master available again |
| Cancel | Reverse or stop a business record while preserving its history |

### Mobile Action Menu

When a row has more than two available actions on a mobile screen, BillFlow places them inside a vertical three-dot menu. This keeps important columns visible while preserving every valid action.

Disabled actions are normally omitted from the compact mobile menu unless they provide necessary workflow context. For example, a Draft quotation may indicate that it must be marked Sent before acceptance.

## Confirmation Dialogs

Actions with significant business impact use confirmation dialogs, including:

- Deactivate
- Accept quotation
- Cancel a document
- Submit or approve attendance
- Reopen approved attendance
- Approve, post, or cancel payroll
- Cancel a site cash or material transaction
- Remove the company logo

Read the dialog carefully. Some actions lock a record or create reversal entries and cannot be treated as ordinary edits afterwards.

## Active and Inactive Masters

Master records such as customers, suppliers, items, units, categories, payment methods, users, employees, locations, and shifts use active/inactive lifecycle control.

- **Active** records can be selected in new transactions.
- **Inactive** records remain in historical documents and reports but are hidden from most new-entry dropdowns.
- **Deactivate** is preferred over deletion because it preserves references.
- **Reactivate** makes the record available again.

## Add New Beside a Dropdown

The Add New icon beside a select opens a compact master form. Save the new master, and BillFlow refreshes the selection list so you can continue the original transaction.

If the icon is missing or disabled, verify Insert permission and the subscription feature.

## Document Preview Versus Table Print

These are different outputs:

- **Table Print** prints a list of visible rows and columns.
- **Document Print** prints a formatted quotation, invoice, receipt, purchase, payment, payroll summary, or payslip.
- Document print uses company details and the uploaded company logo when available.
- Zero-value optional totals such as CGST, SGST, IGST, Discount, and Round Off are omitted from applicable printed documents.
- Draft financial documents may be printed for checking, but they show a `DRAFT` watermark and a no-effect disclaimer. They are not proof that an invoice, receipt, purchase, or payment was posted.
- Cancelled document copies show a `CANCELLED` watermark. Posted documents print without a lifecycle watermark.

If no print window opens, allow pop-ups for the BillFlow site. See [Dashboard, Reports, Printing, and Exports](14-dashboard-reports-printing-and-exports.md).

## Theme Controls

Use the moon/sun control in the top bar or **Settings > Appearance** to change light/dark mode. The selected mode is stored for the current browser/user experience.

The tenant's primary color is stored in company settings and is applied whenever that tenant signs in.

## Unsaved Changes

Most dialogs keep their data only while open. Attendance adds stronger protection: changing the date/department, reloading, leaving the route, or closing the browser with dirty attendance rows triggers an unsaved-changes warning.

## Permission-Aware Controls

Seeing a page does not automatically permit every operation. A user may be able to list and view records but not insert, update, cancel, print, export, or approve them. Contact an administrator when a needed action is disabled.
