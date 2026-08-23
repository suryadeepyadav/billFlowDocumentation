# BillFlow Glossary

## A

**Accepted Quotation**  
A Sent proposal approved by the Customer. It is locked from ordinary editing and can be used to create an Invoice and/or Site.

**Active**  
A master or user available for new work. Active does not mean every related subscription feature or permission is enabled.

**Advance - Customer**  
The unallocated portion of a Receipt. It is recorded against the Customer but not tied to an Invoice. Current BillFlow Receipt UI does not provide a later allocation workflow for this amount.

**Advance - Employee**  
Money paid to an employee before salary and recovered through future Posted payroll runs.

**Advance - Supplier**  
The unallocated portion of a Supplier Payment. It can later be allocated to open Purchases.

**Aging**  
Grouping open receivables/payables by how long they are current or overdue: Current, 1-30, 31-60, 61-90, and 90+ days.

**Allocation**  
Applying a Receipt to an Invoice, a Payment to a Purchase, or a payroll deduction to an Employee Advance.

**Allowance / Earnings**  
Positive payroll lines added to Base and Overtime pay. They may be recurring from Compensation or manual for one run.

**Approval Status**  
Review stage separate from attendance/work status, such as Draft, Submitted, Approved, or Locked.

**Audit Log**  
Read-only history of important creates, updates, approvals, cancellations, and administrative changes.

## B

**Balance Amount**  
Amount still open on an Invoice, Purchase, payroll entry, advance, or other account after valid allocations/payments.

**Base Pay**  
Payroll pay before overtime, additional earnings, and deductions. It is calculated from payable units for Daily Wage or proration/unpaid units for Monthly Salary.

**Bill / Supplier Invoice Number**  
The Supplier's document reference entered on a Purchase or Site Expense. It is different from BillFlow's generated Purchase/Expense number.

**Break Minutes**  
Unpaid/non-working minutes subtracted from elapsed check-in/check-out time in Attendance.

## C

**Cancellation**  
An audited lifecycle action that makes a transaction inactive and reverses its permitted financial/stock effect. It does not erase history.

**Category**  
A classification used to organize Items & Services.

**CGST**  
Central Goods and Services Tax component normally used with SGST for an intra-state transaction.

**Company Settings**  
Tenant-wide legal, contact, address, GST, print-logo, and related business profile.

**Compensation**  
Effective-dated employee wage/salary, standard minutes, overtime, recurring allowances, and recurring deductions.

**Compensation Snapshot**  
Copy of employee compensation stored in a Payroll Entry so historical payroll remains understandable after future rate changes.

**Completed Days**  
A user-entered progress measure in Site Work History. It does not calculate Employee attendance or payroll.

**Contract Value**  
Commercial reference amount on a Site. It is not automatically revenue; Site revenue comes from Posted Site-linked Invoice taxable values.

**Credit Limit**  
Reference amount stored on a Customer. Current BillFlow does not automatically block sales that exceed it.

**Current Cash Balance - Site**  
Operational Site Ledger balance from Opening Cash, Fund Transfers, Site Expenses, and reversals. Customer Receipts/Supplier Payments linked to the Site are broader cash-flow context but do not change this operational ledger.

## D

**Daily Wage**  
Compensation type where Base Pay is Daily Rate multiplied by approved payable attendance units.

**Dashboard Period**  
Month, quarter, financial year, or custom dates used for period-based Dashboard metrics and comparisons.

**Deactivate**  
Hide a reusable master/user from new work while preserving historical references. It is not permanent deletion.

**Deduction**  
Payroll amount subtracted from Gross pay, including recurring lines, manual deductions, and Employee Advance recovery.

**Discount**  
Percentage reduction on a document line before applicable tax calculation. Zero Discount is omitted from clean print totals.

**Document Number**  
Tenant-unique generated reference based on the applicable Sequence, such as Quotation, Invoice, Receipt, Purchase, Site, or Payroll number.

**Due Date**  
Expected settlement date for an Invoice or Purchase. It drives overdue and aging analysis. Payment Terms are stored on masters but due date is explicitly selected on the transaction.

## E

**Effective From**  
Date on which employee Compensation begins to apply.

**Expense Head**  
Reusable classification for Site or General expenses, such as Material Handling, Travel, or Site Labour.

**Export**  
Creation of spreadsheet/CSV output. Shared table Excel normally exports loaded rows; Reports full CSV downloads the complete filtered report.

## F

**Feature / Package Feature**  
Tenant-level subscription entitlement synchronized from SYV Cloud. A feature must be enabled before user permissions can grant useful access.

**Financial Year**  
Named accounting/business period with code, start, end, and active state. It helps setup and numbering; changing it does not rewrite posted documents.

**Free-Text Line**  
A document line not linked to an Item master. BillFlow treats it as a Service, so it does not move stock.

**Fund Transfer - Site**  
Company money sent into Site operational cash. It increases the Site Ledger balance.

## G

**Grace Minutes**  
Shift policy reference stored in BillFlow. Current Attendance does not automatically mark Late or Half Day from it.

**Grand Total**  
Final document total after taxable values, discount, GST, and configured rounding.

**Gross Pay**  
Base Pay + Overtime Pay + recurring/manual Earnings.

**GST**  
Goods and Services Tax. BillFlow can split a line's GST rate into CGST/SGST or apply IGST according to business and party State Codes.

**GST Exclusive**  
Rates are before tax; tax is added to produce the total.

**GST Inclusive**  
Rates include tax; BillFlow derives the taxable and tax portions.

**GSTIN**  
Goods and Services Tax Identification Number. Input is validated/normalized to uppercase where applicable.

## H

**Half Day**  
Attendance status with a configurable payable unit, commonly 0.5. It still requires working times before submission/approval.

**HSN Code**  
Harmonized System of Nomenclature reference generally used for goods/Stock items.

## I

**IGST**  
Integrated GST normally applied to inter-state transactions when valid business and party State Codes differ.

**Inactive**  
Master/user lifecycle state that prevents new selection/access but retains historical data.

**Invoice**  
Posted Customer sales document that creates receivable and, for linked Stock items, reduces Warehouse stock.

**Item**  
Reusable Stock or Service sold/purchased in documents.

**Item Type - Service**  
No stock quantity is tracked.

**Item Type - Stock**  
Quantities are tracked by Warehouse/Site location and changed by posted transactions.

## L

**Ledger**  
Chronological debit/credit style record used to explain a running balance. Site Ledger currently represents operational Site cash.

**License**  
Tenant product entitlement synchronized from SYV Cloud, including active state, expiry, features, and limits.

**Linked Site**  
Site selected on an Invoice, Receipt, Purchase, or Payment for reporting/costing context. Link behavior differs by transaction; it does not always affect Site Ledger cash.

**Low Stock**  
Warehouse quantity at or below an Item's Minimum Stock threshold.

## M

**Manual Adjustment - Payroll**  
One-time earning, deduction, or advance recovery edited for one Payroll Entry.

**Minimum Stock**  
Reorder/alert threshold for an Item's Warehouse quantity.

**Monthly Salary**  
Fixed compensation type prorated for employment overlap and reduced by unpaid attendance units according to Payroll Settings.

**Movement - Stock**  
Immutable quantity event at a location, such as Opening, Purchase In, Sale Out, Adjustment, Site Issue/Return, or reversal.

## N

**Net Payable**  
Gross Pay minus total Deductions, floored at zero.

## O

**Opening Balance - Customer**  
Receivable already owed by the Customer when BillFlow begins. It adds to current Customer outstanding but is not an Invoice allocation row.

**Opening Balance - Supplier**  
Payable already owed to the Supplier when BillFlow begins.

**Opening Cash - Site**  
Initial operational cash entered once when creating a Site. It is immutable and starts Site Ledger balance.

**Opening Stock**  
Initial Warehouse quantity entered during Item setup/migration. It creates an immutable Stock Movement.

**Outstanding**  
Amount still due after valid allocations/payments. Depending on report, it may include opening balance plus open document balances.

**Overtime Candidate**  
Calculated minutes above standard work after minimum and rounding policy. It is not payable until approved.

**Overtime Pay**  
Approved overtime hours multiplied by a fixed hourly rate or calculated multiplier rate for an overtime-eligible employee.

## P

**PAN**  
Permanent Account Number. Validated/normalized to uppercase where applicable.

**Partially Paid**  
Some payment/receipt allocation exists but outstanding remains.

**Payable Day Units**  
Payroll value assigned to attendance status: commonly Present 1, Half Day 0.5, Paid Leave 1, Unpaid/Absent 0. Configurable statuses use Payroll Settings.

**Payment - Supplier**  
Money paid to a Supplier. It may be allocated to Purchases or retained as unallocated Supplier advance.

**Payment Method**  
Reusable way money moves, such as Cash, Bank, UPI, Cheque, Card, or Other. Payroll uses its own method value list but follows the same business idea.

**Payment Status**  
Settlement state separate from document status: Pending/Partial/Paid for Invoice/Purchase, or Unpaid/Partially Paid/Paid for payroll entries.

**Payroll Run**  
Controlled salary calculation for a non-overlapping date period.

**Posted**  
Active transaction state where financial, balance, stock, or payroll effects have been recognized.

**Profit Margin**  
Site Profit divided by tax-excluded Site revenue, expressed as a percentage where revenue is non-zero.

**Purchase**  
Posted Supplier document that creates payable and adds Stock to Warehouse or a selected Site.

## Q

**Quotation**  
Customer proposal that can progress Draft -> Sent -> Accepted/Rejected/Cancelled. It does not create receivable or stock movement.

## R

**Reactivate**  
Return an Inactive reusable master/user/employee/Site to normal eligible use, subject to business rules.

**Receipt**  
Money received from a Customer. Allocation reduces Invoice balance; remainder is Customer advance.

**Recurring Allowance/Deduction**  
Compensation line automatically copied into each applicable calculated Payroll Entry.

**Reference Number**  
External bank, UPI, cheque, Supplier, or other traceable identifier.

**Reopen Attendance**  
Return Approved attendance to Draft with a reason, permitted only before Payroll locks it.

**Reversal**  
Opposite transaction/event created or applied when a Posted record is cancelled. A reversal preserves both the original and correction history.

**Role**  
Built-in permission template such as Admin, Accountant, Site Manager, or HR Manager. Saved user permissions can be customized beyond the template.

## S

**SAC Code**  
Services Accounting Code generally used for Service items.

**Salary Divisor**  
26, 30, calendar days, or working days used for monthly unpaid deduction and hourly overtime-rate calculations.

**Salary Payment**  
Payment against a Posted payroll employee entry. Supports partial settlement and audited cancellation.

**Sequence**  
Numbering configuration with document type, prefix, financial-year code, current number, and padding.

**SGST**  
State GST component normally paired with CGST for intra-state transactions.

**Shift**  
Reusable attendance schedule containing start/end times, standard minutes, break, grace, threshold, and night-shift flag.

**Site**  
Customer-linked project/work location used for operational cash, materials, expenses, work history, and profitability.

**Site Expense**  
Posted operational expense that reduces Site cash and contributes to Site cost.

**Site Material Issue/Return**  
Stock transfer between Warehouse and Site that changes location quantities and Site material cost.

**Site Work History**  
Day-by-day operational work record. It is not connected to employee attendance/payroll.

**State Code**  
GST jurisdiction code used to decide intra-state CGST/SGST versus inter-state IGST.

**Stock Adjustment**  
Authorized manual Warehouse quantity increase/decrease for verified variance or correction.

**Subscription Limit**  
Maximum licensed usage value, such as users, synchronized from SYV Cloud.

**Supplier**  
Vendor from whom goods/services are purchased.

## T

**Taxable Amount / Taxable Value**  
Value before GST. Dashboard sales/project revenue and purchase/project cost commonly use taxable values to avoid treating GST as income/cost.

**Tenant**  
One subscribed company/workspace. Tenant data, settings, users, sequences, and permissions are isolated from other tenants.

**Tenant ID**  
Unique workspace identifier. It is derived through the authenticated flow and is not shown as a normal login field.

## U

**Unallocated Amount**  
Receipt/Payment amount not tied to an Invoice/Purchase. It represents party advance.

**Unit**  
Measurement used for Items, such as Nos, Kg, Meter, or Hour, with allowed decimal precision.

## W

**Warehouse**  
Default central stock location. Invoice Stock always leaves Warehouse; a Purchase without Site enters Warehouse.

**Work History**  
See Site Work History.

**Work Location**  
Independent attendance location such as Head Office or Workshop. It is not a BillFlow Site.

**Worked Minutes**  
Elapsed check-in/check-out minutes less Break. Regular and overtime candidate minutes are derived from it.

Return to the [Documentation Home](README.md) or continue to [Troubleshooting and FAQ](18-troubleshooting-and-faq.md).
