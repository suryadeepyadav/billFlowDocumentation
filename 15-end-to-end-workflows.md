# End-to-End Workflows

## Why This Guide Exists

BillFlow modules are connected business records. This guide shows the recommended order for common work and explains what each step changes.

Use the module guides for every field and status. Use this guide when asking, "What should happen next?"

# One-Time Company Setup

Complete setup before production transactions.

## 1. Company and Tax

1. Open **Settings > Company**.
2. Enter legal/company contact and address information.
3. Upload the company logo.
4. Open **Settings > Tax**.
5. Configure tax enabled, GST registration, GSTIN, PAN, business state/code, calculation mode, and defaults.
6. Add invoice terms.

Correct business State Code and party State Code are essential for CGST/SGST versus IGST.

## 2. Financial Year and Sequences

1. Create the current Financial Year.
2. Mark it Active.
3. Review every used sequence prefix, financial-year code, current number, and padding.
4. Check each sequence Preview before transactions begin.

Do not casually reset Current Number after documents exist.

## 3. Common Masters

Create in this practical order:

1. Units
2. Categories
3. Items & Services
4. Payment Methods
5. Expense Heads
6. Customers
7. Suppliers

For workforce usage, also create Work Locations, Shifts, and Employees.

## 4. Users and Permissions

1. Create named users.
2. Choose role defaults.
3. Customize permission matrices.
4. Test each user's normal workflow.

## 5. Opening Data

- Customer Opening Balance represents pre-BillFlow receivable.
- Supplier Opening Balance represents pre-BillFlow payable.
- Item Opening Stock creates the initial Warehouse movement.
- Site Opening Cash creates Site's initial operational cash.

Enter opening values once and preserve evidence of how they were calculated.

# Quote-to-Cash Workflow

## Purpose

Move from a customer proposal to accepted work, billing, collection, and outstanding tracking.

## Recommended Flow

```text
Customer -> Quotation Draft -> Sent -> Accepted -> Invoice and/or Site -> Receipt allocation
```

## Step 1: Add Customer

Create the Customer with accurate State/State Code, GSTIN, address, opening balance, and commercial notes.

While creating a Quotation or Invoice, use the plus icon beside Customer to add a missing Customer. After saving, return to the prior workflow and select the new record.

## Step 2: Create Quotation

1. Select Customer and optional Site.
2. Enter quotation date and validity.
3. Add Item/Service lines.
4. Verify tax, discount, totals, terms, and notes.
5. Save as Draft while preparing.
6. Print/review before sending.

Quotation does not create revenue, receivable, or stock movement.

## Step 3: Send and Accept

1. Move the completed Draft to Sent.
2. Record customer follow-up outside/inside notes as company practice requires.
3. Accept only after customer approval.
4. Confirm Accept because Accepted quotations are locked from ordinary editing.

Accepted is valid only for a Sent quotation; a Draft is still internal preparation.

## Step 4A: Convert to Invoice

Create an Invoice from the Accepted quotation. Review the copied Customer, Site, lines, tax, dates, and amounts before posting.

Posting the Invoice:

- Creates a Customer receivable.
- Reduces Warehouse stock for Stock items.
- Adds Site revenue/costing context if linked to a Site.
- Cannot be edited like a Draft.

## Step 4B: Create a Site

When accepted work becomes a project/site:

1. Use Create Site on the Accepted quotation.
2. Enter Site name, contract/opening cash, dates, manager, and notes.
3. Continue Site operations in Site Management.

A quotation may support Site creation and/or Invoice conversion according to business need and existing links.

## Step 5: Record Receipt

1. Select the same Customer.
2. Enter receipt date, amount, method, and reference.
3. Allocate to one or more open Invoices.
4. Verify total allocation does not exceed receipt amount or invoice balance.
5. Save and print the receipt.

Effects:

- Allocated amount reduces Invoice balance.
- Invoice becomes Partially Paid or Paid.
- Any remainder becomes unallocated Customer advance.

Customer advances are not automatically allocated later in the current Receipt UI. Prefer allocating correctly during entry and monitor unallocated receipt alerts/reports.

## Step 6: Monitor Collection

Use:

- Dashboard Receivables and aging
- Customer Outstanding report
- Sales report
- Receipts report
- Invoice payment status

`Outstanding = Opening Balance + Posted Invoice balances`. An unallocated receipt is tracked separately and is not automatically netted into an Invoice balance.

# Direct Invoice-to-Receipt Workflow

Use direct Invoice creation when no quotation is required.

```text
Customer -> Posted Invoice -> Receipt allocation -> Paid/Partially Paid
```

Review tax and Warehouse stock before saving because the Invoice posts immediately.

# Procure-to-Pay Workflow

## Purpose

Record Supplier purchases, receive stock, track payables, and pay Suppliers.

## Recommended Flow

```text
Supplier -> Posted Purchase -> Stock receipt -> Supplier Payment allocation
```

## Step 1: Add Supplier

Record Supplier State/State Code, GSTIN, address, opening balance, payment terms, and contacts.

Use the plus icon beside Supplier in Purchase creation when a new Supplier is needed.

## Step 2: Create Purchase

1. Select Supplier.
2. Select Site only when stock is received directly at that Site.
3. Enter purchase date, due date, and supplier invoice number.
4. Add Stock/Service lines.
5. Verify tax and totals.
6. Save.

Posting the Purchase:

- Creates Supplier payable.
- Adds Stock items to Warehouse when no Site is selected.
- Adds Stock items directly to the selected Site when Site is selected.
- Adds direct purchase cost to linked Site costing.

## Step 3: Record Supplier Payment

1. Select Supplier.
2. Enter payment date, amount, method, and reference.
3. Allocate to one or more open Purchases.
4. Save.

Effects:

- Allocated amount reduces Purchase balance.
- Purchase becomes Partially Paid or Paid.
- Remainder becomes Supplier advance.

Unlike Customer Receipts, BillFlow currently provides **Allocate Supplier Advance** later. Use it to apply an unallocated Payment balance to open Purchases.

## Step 4: Monitor Payables

Use Dashboard Payables/aging and Purchases, Payments, and Supplier Outstanding reports.

Supplier outstanding includes opening balance, posted purchase balances, and payments. A negative net may represent Supplier advance.

# Inventory Workflow

## Setup

```text
Unit + Category -> Item -> Opening stock/adjustment -> Transactions -> Stock reports
```

## Normal Stock Sources

- Item opening stock
- Purchase into Warehouse or Site
- Invoice out from Warehouse
- Warehouse adjustment in/out
- Site material issue/return
- Transaction cancellation reversals

## Routine Process

1. Create Items with correct Stock/Service type and Unit.
2. Enter opening stock only for initial migration.
3. Receive new stock through Purchases.
4. Move Warehouse stock to/from Sites through Site Materials.
5. Use Adjust Stock only for verified corrections, damage, count variance, or non-purchase movement.
6. Review Stock Summary and Stock Movements.
7. Investigate low/out-of-stock alerts.

Do not use Service lines when stock tracking is required. Free-text document lines are treated as Service and do not move stock.

# Site Operations Workflow

## Purpose

Track a customer project/location, operational Site cash, materials, work history, direct cost, and profitability.

## Recommended Flow

```text
Site -> Fund cash -> Record expenses -> Issue/return materials -> Work history -> Review costing/ledger
```

## Step 1: Create and Activate Site

Create directly or from an Accepted quotation. Confirm Customer, status, start/end dates, contract context, and opening cash.

Only active Sites with Active status accept normal operational postings.

## Step 2: Fund Site Cash

Record a Fund Transfer when company funds are sent to the Site. This increases the operational Site Ledger cash balance.

## Step 3: Record Site Expense

Select an Expense Head and enter amount/date/vendor/bill information. The Site must have enough operational cash. Posting reduces Site cash; cancellation restores it.

## Step 4: Issue or Return Material

- Issue transfers Stock from Warehouse to Site.
- Return transfers Stock from Site back to Warehouse.

Use Stock items only and verify quantity/rate. These movements affect Site material cost and location balances.

## Step 5: Maintain Work History

Record day-by-day Work Name, location, date/times, worker count, completed days, status, details, and remarks.

This is operational history. Worker count is not connected to Employee attendance/payroll.

## Step 6: Review Site

Use Site tabs and reports to compare:

- Tax-excluded Invoice revenue
- Material cost
- Direct Purchase cost
- Site Expense cost
- Profit/loss and margin
- Operational Site cash
- Customer receipts and Supplier payments as broader cash-flow context

Do not confuse customer-linked Receipt or supplier-linked Payment with operational Site Ledger cash. Only Opening Cash, Fund Transfers, Site Expenses, and their reversals change that ledger.

# Attendance-to-Payroll Workflow

## Recommended Flow

```text
Employee + Compensation -> Daily Attendance -> Submit -> Approve -> Payroll Calculate -> Approve -> Post -> Salary Payment
```

## Step 1: Prepare Workforce Masters

1. Configure Payroll Settings.
2. Add Work Locations and Shifts.
3. Add Employees with correct joining dates.
4. Add initial/effective Compensation.
5. Configure overtime eligibility and method.

## Step 2: Enter Daily Attendance

1. Select date/department.
2. Mark all Present only as a shortcut.
3. Correct leave/absence/half-day rows.
4. Enter check-in/out and optional Shift/Location/Break.
5. Review worked time and overtime candidate.
6. Save Draft.

## Step 3: Submit and Approve

- Submit complete attendance for review.
- Approve attendance and the chosen overtime minutes.
- Reopen with a reason if correction is needed before payroll.

Only Approved attendance enters payroll.

## Step 4: Calculate Payroll

1. Create the non-overlapping run period.
2. Calculate.
3. Resolve missing compensation/unapproved attendance warnings.
4. Review daily/monthly base calculation.
5. Review overtime rate/pay.
6. Review recurring/manual earnings, deductions, and advance recovery.

## Step 5: Approve and Post

- Approve locks included attendance.
- Post creates salary balances and applies advance recovery.

## Step 6: Pay Salary

Record partial or full salary payments against Posted employee payroll entries. Print payslips and monitor Outstanding.

# Inline Add-New Workflow

To reduce navigation, supported select fields have an Add icon:

- Quotation/Invoice: Add Customer and Add Item
- Purchase: Add Supplier and Add Item
- Item: Add Category and Add Unit
- Other supported master selectors where creation permission is available

Recommended use:

1. Preserve the current unfinished form.
2. Select Add beside the missing option.
3. Complete and save the master.
4. Return to the original route/workflow.
5. Refresh/reopen the selector if necessary.
6. Select the new record and continue.

The Add icon appears only when the user has access to create the related master and the subscription feature is enabled.

# Correction and Reversal Order

BillFlow preserves history by cancelling/reversing dependent records rather than deleting posted transactions.

## Sales Reversal

```text
Cancel Receipt allocations/Receipts -> Cancel Invoice -> Cancel Quotation when allowed
```

- Invoice cannot be cancelled while amount has been received.
- Invoice cancellation reverses Warehouse Stock items.
- Accepted Quotation cancellation is blocked when linked to an Invoice or Site.

## Purchase Reversal

```text
Cancel Supplier Payment allocations/Payments -> Ensure original-location stock exists -> Cancel Purchase
```

- Purchase cannot be cancelled while amount has been paid.
- Stock reversal must be possible at the original Warehouse/Site location.

## Site Reversal

- Cancel Site Expense to restore Site cash.
- Cancel Fund Transfer only when enough Site cash remains to reverse it.
- Cancel Site Material only when required stock exists at the reversal source.
- Cancel Work History with a reason; it remains in history.

## Payroll Reversal

```text
Cancel Salary Payments -> Cancel Payroll Run -> Reopen Attendance -> Correct -> Recalculate
```

Payroll cancellation reverses advance recoveries/salary balances and unlocks attendance back to Approved.

# Daily, Weekly, and Monthly Checklist

## Daily

- Enter/approve attendance.
- Record customer receipts and supplier payments.
- Record purchases/invoices created that day.
- Record Site fund/expense/material/work transactions.
- Review Dashboard attention alerts.

## Weekly

- Follow up Sent/expiring Quotations.
- Review overdue Receivables and Payables.
- Allocate Supplier advances.
- Investigate unallocated Customer receipts.
- Review low/out-of-stock items.
- Review Site cash and losses.
- Review pending attendance approvals.

## Month/Period End

- Complete and approve attendance.
- Calculate, review, approve, and post Payroll.
- Reconcile salary payments and employee advances.
- Reconcile Sales, Purchases, Receipts, and Payments reports.
- Review Customer/Supplier outstanding.
- Review Stock and Stock Movements.
- Review Site P&L and Site Cash Flow.
- Download full CSV reports for records as required.
- Review Audit activity and subscription status.

Continue with [Status Reference](16-status-reference.md).
