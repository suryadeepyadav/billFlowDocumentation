# Troubleshooting and FAQ

## How to Troubleshoot Safely

Before changing or cancelling data:

1. Read the complete message shown by BillFlow.
2. Confirm the tenant/company and signed-in user.
3. Confirm the module, document number, status, and selected date.
4. Check active Search/Filters and subscription/permissions.
5. Refresh once and retry the exact valid action.
6. Follow dependency-aware reversal steps instead of deleting data.

Do not repeatedly submit the same transaction when the first request may have succeeded. Refresh the list and search the generated document number first.

# Login and Access

## Why Is There No Tenant ID Field on Login?

This is intentional. Use the Username and Password issued for the tenant. The authenticated session carries the tenant identity; users should not type or switch Tenant ID on the login page.

## I Cannot Log In

Check:

- Username spelling and case according to company practice
- Password and Caps Lock
- User Active state
- Tenant/subscription Active state and expiry
- Whether an administrator recently reset the password
- Correct BillFlow deployment/domain

Ask an Admin to reactivate/reset the account. Do not send passwords in screenshots or support messages.

## I Was Signed Out After an Admin Change

Deactivating a user signs out active sessions. Password or access changes may also require a fresh login. Sign in with current credentials after the administrator confirms access.

## A Menu Is Missing

The menu requires both subscription entitlement and user View permission.

1. Check **Settings > Subscription** for the feature.
2. Check dependency features, such as Employees + Attendance + Payroll.
3. Check **Users & Permissions** for module View permission.
4. Sign out/in or refresh after changes.

## I Can Open a Page but an Action Returns 403 / No Permission

View permission may open the page while the action needs Insert, Update, Delete, Approve, Cancel, Print, or Export.

Ask an Admin to inspect the exact module/action checkbox. A role label alone does not guarantee all actions because per-user permissions are customizable.

## Everything Returns 403

Likely causes:

- Subscription inactive or expired
- Required feature disabled
- User deactivated
- Permission record missing/incorrect
- Stale session after access changes

Use the protected First Admin to repair permissions if needed, then sign in again.

## License Expired or Feature Not Included

BillFlow cannot change package entitlement locally. An authorized operator must update/renew the package in SYV Cloud and synchronize it. Verify Product code, active state, expiry, package features, and last sync.

# Lists, Search, and Mobile Actions

## Backend Has Data but the List Looks Empty

Check:

- Search text
- Status/Active filter
- Advanced filter rows and AND/OR mode
- Date range
- Current page after filters changed
- Selected columns
- Correct tenant/user permissions

Clear filters, reset columns if needed, and Refresh. Inactive masters may be hidden from active-only selectors even when still present in history.

## I Cannot See All Action Icons on Mobile

When a row has more than two actions, BillFlow places them in a vertical three-dot menu on mobile. Open the menu to see enabled and disabled actions. Disabled actions normally indicate missing permission or invalid record status/dependency.

## Why Does Excel Contain Only One Page?

Shared table Excel exports currently loaded/displayed rows. On server-paged lists this normally means the current page.

For complete report data, open Reports, apply filters, and use **Download full CSV report**.

# Forms and Dropdowns

## What Do Required and Optional Mean?

- Required fields must contain a valid value before Save/Submit.
- Optional fields can remain blank, but may be important for tax, reporting, printing, or calculations.
- Conditional fields become required only for a selected status/method, such as check-in/out for Present attendance.

Use the field table in each module guide before initial setup.

## A Value Is Missing from a Dropdown

Possible reasons:

- Master is Inactive.
- Subscription feature is disabled.
- User lacks View/List permission.
- The selector accepts only a subtype, such as Stock items for Site Material.
- Site is not operational Active.
- Data was created in another browser tab and options need Refresh.

## How Do I Add a Missing Customer, Supplier, Item, Category, or Unit?

Use the plus icon beside supported selectors. Save the new master, return to the prior workflow, refresh options when necessary, then select it.

The plus icon is hidden/disabled without creation permission.

## GSTIN or PAN Changes to Uppercase

This is expected. BillFlow normalizes these identifiers to uppercase and validates their format.

# GST and Totals

## Why Is IGST Calculated Instead of CGST/SGST?

BillFlow compares Company Business State Code with the Customer/Supplier State Code.

- Different valid codes: IGST.
- Same code: CGST + SGST split.

Check **Settings > Tax** and the selected party master. Correct wrong State Code data, then recreate/recalculate an editable document. Do not alter Posted documents outside their cancellation/re-entry workflow.

## Why Is Tax Not Calculated?

Check:

- Tax Enabled is on.
- GST Registered is on when GST should apply.
- GST Calculation mode is correct.
- Item/line GST rate is greater than zero.
- Quantity/rate are valid.
- Company and party tax details are correct.

## Why Are CGST/SGST/IGST or Discount Missing from Print?

BillFlow intentionally hides optional tax/discount/charge rows when their value is zero. Only applicable non-zero values are printed.

## Why Does Dashboard Revenue Differ from Invoice Grand Total?

Dashboard sales/project revenue uses Posted taxable value excluding GST. Invoice Grand Total includes GST and possibly rounding. GST collected is not business revenue.

# Quotations

## Why Can I Not Accept a Draft Quotation?

Draft means internal preparation. Move it to Sent after review, then Accept after Customer approval.

## Why Is an Accepted Quotation Read-Only?

Acceptance is a controlled commitment. The confirmation warns that ordinary editing will stop. Create the required Invoice/Site or use cancellation only when no blocking links exist.

## Why Can I Not Cancel an Accepted Quotation?

Cancellation is blocked when an Invoice or Site is linked. Resolve downstream records according to business policy; do not remove references manually.

## Does a Quotation Move Stock or Create Outstanding?

No. A Quotation is a proposal. Posted Invoice creates receivable and Stock movement.

# Invoices and Receipts

## Why Can I Not Edit a Saved Invoice?

Invoices post immediately. They create receivable and may reduce Warehouse stock. To correct a material mistake, cancel dependencies and the Invoice, then create a replacement.

## Why Can I Not Cancel an Invoice?

An Invoice with allocated Receipt amount cannot be cancelled. Cancel related Receipts first. Stock reversal must also remain valid.

## Receipt Is Larger Than Selected Invoice Balance

Reduce the allocation or allocate remaining amount to other open Invoices. Any unallocated remainder becomes Customer advance.

## Can I Allocate an Existing Customer Advance Later?

Current BillFlow UI does not provide a later Customer Receipt advance-allocation action. The advance still reduces the Customer's overall account balance but does not change an individual Invoice payment status. Allocate correctly during Receipt entry and monitor unallocated receipt reporting. Contact an authorized administrator for correction policy rather than creating duplicate Receipts.

## Why Does Customer Outstanding Still Include Opening Balance?

Customer Opening Balance is a pre-BillFlow receivable and is not an Invoice allocation row. It remains part of outstanding reporting unless handled through the organization's migration/accounting correction process.

# Purchases and Payments

## Why Can I Not Edit a Saved Purchase?

Purchases post immediately and may add stock/create payable. Correct through controlled cancellation and replacement.

## Why Can I Not Cancel a Purchase?

Check both dependencies:

1. Cancel allocated Supplier Payments first.
2. Ensure enough Stock remains at the original receipt location (Warehouse or selected Site) for reversal.

If stock has already been sold, issued, returned, or adjusted, restore the legitimate movement sequence before cancellation.

## How Do I Use Supplier Advance?

Open Payments and use **Allocate Supplier Advance** on a Posted Payment with unallocated balance. Select open Purchases and allocate within their balances and the available advance.

## Supplier Outstanding Is Negative

A negative net can indicate Supplier advance: payments exceed opening payable plus current Purchase balances. Review Payment allocations and Supplier Outstanding report.

# Inventory

## Stock Item Quantity Did Not Change

Check:

- Line is linked to an Item master.
- Item Type is Stock, not Service.
- Source transaction is Posted, not Quotation/Draft/Cancelled.
- Correct location is being viewed.

Free-text lines are Services and do not move stock.

## Purchase Stock Is Not in Warehouse

A Purchase linked to a Site receives Stock directly at that Site. A Purchase with no Site receives into Warehouse.

## Invoice Linked to a Site Reduced Warehouse

This is expected. Sales Invoice Stock always leaves Warehouse in the current model, even when the Invoice is linked to a Site.

## Why Can I Not Change Item Type or Opening Stock?

After an Item has Stock Movements, those foundational values are locked to preserve history. Use Stock Adjustment for a verified quantity correction.

## Insufficient Stock

The requested OUT, Invoice, Site Issue/Return reversal, or Purchase cancellation would make a location negative.

Review Stock Summary and Stock Movements for the Item/location. Correct the real preceding transaction; do not add a false adjustment simply to bypass validation.

## Low Stock Looks Wrong

Low Stock compares Warehouse quantity with Minimum Stock. Quantity at Sites is shown separately and does not protect Warehouse from a low-stock warning.

# Sites

## Why Can I Not Post a Site Transaction?

The Site must be lifecycle Active and have Active status. Draft, On Hold, Completed, Cancelled, or Inactive Sites may block normal postings.

## Insufficient Site Cash

Site Expense would reduce operational cash below allowed balance. Record a real Fund Transfer or correct an erroneous prior Site transaction first.

Customer Receipt linked to the Site does not fund operational Site Ledger cash.

## Why Did a Site-Linked Receipt/Payment Not Change Site Cash?

This is intentional. Site operational cash changes through Opening Cash, Fund Transfers, Site Expenses, and reversals. Customer Receipts and Supplier Payments are shown as broader Site cash-flow/costing context.

## Why Can I Not Cancel a Fund Transfer?

Reversal would remove cash already spent. Cancel dependent Site Expenses or otherwise restore genuine available Site cash before reversing the transfer.

## Site Material Return or Cancellation Fails

The reversal source location lacks enough Stock. Review Issue/Return movements and current Warehouse/Site balances.

## Is Site Work History Connected to Attendance?

No. Worker Count and Completed Days are operational Site notes. Employees, Attendance, and Payroll are independent modules.

# Attendance

## Are Shift, Work Location, and Break Required?

No. They are optional. **Show all columns** displays/hides them without erasing data.

Present and Half-Day attendance requires valid Check-in and Check-out before Submit/Approve. Draft can be saved while incomplete.

## Save Created Draft, Not Approved Attendance

This is expected. Use Save & Submit, then Approve; or authorized **Save & approve all** after reviewing the batch.

## Why Is Save & Approve All Missing?

The user needs Attendance Approve permission. It is permission-based, not merely based on the visible role name.

## Overtime Is Zero

Check:

- Check-in/out and Break
- Shift or global Standard daily minutes
- Minimum overtime threshold
- Rounding interval
- Overtime approval choice
- Employee Compensation Overtime eligible and method

Attendance first calculates candidate minutes. Payroll pays only Approved overtime for an eligible employee.

## Check-Out Earlier Than Check-In Produced a Long Shift

BillFlow treats check-out less than/equal to check-in as next-day overnight work. Correct accidental reversed time before approval.

## Submitted Attendance Is Read-Only

Submitted data waits for an approver. Current Reopen action applies to Approved attendance. Review before Submit and ask an authorized supervisor to complete the workflow.

## Attendance Is Locked

An Approved Payroll Run locked it. Cancel salary payments, cancel the payroll run with reason, then Reopen the returned Approved attendance. See [Payroll](12-payroll.md).

# Payroll

## Employee Is Missing from Payroll

Check:

- Joining/leaving dates overlap the run.
- Effective Compensation exists for the period.
- Attendance is Approved.
- Employee/records belong to the same tenant.

Calculate warnings identify missing compensation and excluded unapproved attendance.

## Payroll Amount Is Zero or Lower Than Expected

Review:

- Daily Wage vs Monthly Salary
- Base rate and effective date
- Approved payable attendance units
- Unpaid units
- Salary divisor
- Joining/leaving proration
- Approved overtime and eligibility
- Recurring/manual deductions
- Employee Advance recovery

Use the Payroll Entry details rather than comparing only the final Net amount.

## Cannot Create Payroll: Period Overlaps

A non-cancelled Payroll Run already covers part of the selected dates. Open existing runs and use a non-overlapping period or cancel the incorrect run using the controlled workflow.

## Cannot Approve Payroll

Common causes:

- Run has not been Calculated.
- No employee entries exist.
- Deductions exceed Gross.
- Attendance in the period is unresolved.
- User lacks Payroll Approve permission.

Resolve warnings and recalculate.

## Record Salary Payment Is Disabled

The run must be Posted, the employee must have Outstanding amount, and the user needs Payroll Insert permission.

## Cannot Cancel Payroll

Cancel all Posted Salary Payments for the run first. Then cancel Payroll with a reason. BillFlow reverses salary balances/advance recovery and unlocks attendance.

## Cannot Cancel Employee Advance

An advance can be cancelled only before any payroll recovery is posted. If recovery exists, resolve the related payroll through its controlled cancellation workflow.

# Company Logo, Appearance, and Printing

## Logo Upload Fails

Use PNG, JPEG, or WebP no larger than 2 MB. Confirm the file is a real image and the user has Settings Update permission.

Uploading a replacement removes the previous tenant logo file after the new upload succeeds. Delete Logo asks for confirmation.

## Print Window Does Not Open

Allow pop-ups for the BillFlow domain. Retry from the document's Print action. Also verify browser printing is available.

## Logo or Company Details Are Wrong on Print

Update **Settings > Company**, then reopen/reprint the document. Verify the image and legal/GST fields before distribution.

## Primary Color Is Different for Everyone

Primary Color is tenant-wide and stored in backend settings. Saving it changes the portal appearance for tenant users after settings load/refresh.

## Light/Dark Mode Did Not Follow Another User

Light/Dark preference is browser/user-device local in the current implementation. It is intentionally not stored tenant-wide like Primary Color.

# Numbering and Financial Years

## Document Number Is Unexpected

Check:

- Correct Sequence type
- Prefix
- Financial-year code
- Current Number
- Padding and Preview
- Active Financial Year context

Do not edit sequences merely to make one document look different. Existing posted numbers remain unchanged.

## Duplicate or Number Conflict

Another transaction may already use the generated number, or Current Number may have been moved backward. Review sequence history and increase to a safe next number. Never renumber posted records manually.

# When Contacting Support

Provide:

- BillFlow deployment/domain and app version if shown
- Tenant ID/company name (not license secret)
- User name and role (not password)
- Module and exact action
- Document/employee/Site number
- Date/time and timezone
- Exact error message and HTTP status if available
- Screenshot with sensitive data redacted
- Steps that reproduce the issue
- Whether it affects one user or all users

Never provide passwords, JWT tokens, database credentials, cloud sync secret, license key, full bank account data, or private employee information in an unsecured message.

Return to the [Documentation Home](README.md).
