# Status Reference

## How to Use This Guide

BillFlow records can have more than one kind of status. Always identify which status you are reading:

- **Lifecycle status**: Active/Inactive master availability.
- **Document status**: Draft, Posted, Cancelled, and similar transaction state.
- **Payment status**: Whether a posted amount is unpaid, partial, or paid.
- **Approval status**: Attendance/payroll review stage.
- **Work status**: Operational progress of Site Work History.

A Posted Invoice can be Partially Paid; these are two separate statuses.

# Common Master Lifecycle

Applies to Customers, Suppliers, Items, Categories, Units, Payment Methods, Work Locations, Shifts, Users, and similar reusable masters.

| State | Meaning |
| --- | --- |
| Active | Available for normal new selection and use |
| Inactive | Hidden from active selectors/new work; historical references remain |

Use Deactivate/Reactivate. BillFlow generally avoids permanent deletion so old documents remain understandable.

# Tenant and Subscription

## Tenant Status

| Status | Meaning |
| --- | --- |
| Pending | Tenant registration exists but activation is incomplete |
| Active | Tenant is operational, subject to subscription |
| Suspended | Tenant access is administratively suspended |

## Subscription State

| State | Meaning |
| --- | --- |
| Active | Entitlement is enabled and within expiry |
| Inactive | License has been disabled by centralized administration |
| Expired | Expiry date has passed |

Subscription feature flags and user permissions still determine which modules can be used.

# Quotations

| Status | Meaning | Typical next action |
| --- | --- | --- |
| Draft | Internal proposal preparation | Edit, print/review, move to Sent |
| Sent | Proposal delivered to Customer | Accept, reject according to workflow, or cancel |
| Accepted | Customer approved; quotation is locked | Create Invoice and/or Site |
| Rejected | Customer declined | Retain for pipeline/history |
| Cancelled | Quotation intentionally withdrawn/reversed | View history only |

Acceptance is valid from Sent, not Draft. Accepted cancellation is restricted when a linked Invoice or Site exists.

# Sales Invoices

## Document Status

| Status | Meaning |
| --- | --- |
| Posted | Active receivable and, for Stock items, Warehouse stock movement exists |
| Cancelled | Receivable and eligible stock effect have been reversed |

## Payment Status

| Status | Meaning |
| --- | --- |
| Pending | No Receipt allocation has reduced the Invoice balance |
| Partial | Some amount is allocated; balance remains |
| Paid | Allocated amount covers the Invoice total |

An Invoice cannot be cancelled while its paid amount is greater than zero. Cancel related Receipts first.

# Receipts

| Status | Meaning |
| --- | --- |
| Posted | Active Customer receipt/allocation |
| Cancelled | Receipt allocations and effects reversed |

Allocation values are separate:

- Allocated amount: Applied to Invoices.
- Unallocated amount: Customer advance not tied to an Invoice.

# Purchases

## Document Status

| Status | Meaning |
| --- | --- |
| Posted | Active Supplier payable and eligible Stock receipt exists |
| Cancelled | Payable and eligible stock effect reversed |

## Payment Status

| Status | Meaning |
| --- | --- |
| Pending | No Payment allocation has reduced the Purchase balance |
| Partial | Some amount is allocated; balance remains |
| Paid | Allocated amount covers the Purchase total |

A Purchase cannot be cancelled while its paid amount is greater than zero. Stock must also exist at the original receipt location for reversal.

# Supplier Payments

| Status | Meaning |
| --- | --- |
| Posted | Active Supplier Payment/allocation |
| Cancelled | Allocations and payment effect reversed |

Unallocated amount is Supplier advance and may later be allocated to open Purchases.

# Sites

Sites have both `status` and an Active/Inactive lifecycle flag.

| Status | Meaning |
| --- | --- |
| Draft | Site record is being prepared |
| Active | Site is operational and can accept normal postings when also Active in lifecycle |
| On Hold | Work temporarily paused |
| Completed | Operational work completed; history remains |
| Cancelled | Site cancelled/deactivated |

Normal Site postings require the Site to be lifecycle Active and have Active status. Reactivation returns the Site to operational Active status.

# Site Transactions

Site Fund Transfers, Site Expenses, and Site Materials use:

| Status | Meaning |
| --- | --- |
| Posted | Active transaction included in ledger/stock/costing as applicable |
| Cancelled | Reversal posted; original retained for audit |

Site Material also has a transaction type:

| Type | Meaning |
| --- | --- |
| Issue | Warehouse stock transferred to Site |
| Return | Site stock transferred to Warehouse |

# Site Work History

| Status | Meaning |
| --- | --- |
| Pending | Work planned/not begun |
| In Progress | Work currently underway |
| On Hold | Work paused |
| Completed | Work entry/activity completed |
| Cancelled | Entry cancelled with reason and locked from editing |

Work History status does not alter Site status, Inventory, Attendance, Payroll, or Site Ledger.

# Employees and Compensation

## Employee Status

| Status | Meaning |
| --- | --- |
| Active | Employee available for attendance/payroll eligibility |
| Inactive | Employee removed from new attendance; history remains |

Deactivation sets a Leaving Date when one is absent. Reactivation clears it.

## Compensation Status

| Status | Meaning |
| --- | --- |
| Active | Current/effective compensation record |
| Superseded | Historical rate replaced by a later effective compensation |

Payroll captures a snapshot of the compensation it uses.

# Attendance

## Attendance Status

| Status | Meaning | Default payable units |
| --- | --- | --- |
| Present | Worked full day | 1 |
| Absent | Did not work, unpaid | 0 |
| Half Day | Partial working day | 0.5 |
| Paid Leave | Paid approved leave | 1 |
| Unpaid Leave | Approved leave without pay | 0 |
| Week Off | Scheduled paid rest day | 1 |
| Holiday | Paid holiday | 1 |

Configurable statuses may use different payable units from the defaults.

## Approval Status

| Status | Meaning | Editable? | Payroll eligible? |
| --- | --- | --- | --- |
| Draft | Entry in progress | Yes | No |
| Submitted | Waiting for approval | No | No |
| Approved | Accepted attendance/overtime | After Reopen | Yes |
| Locked | Included in approved payroll | No | Yes/already linked |

# Payroll Runs

| Status | Meaning | Typical next action |
| --- | --- | --- |
| Draft | Period created | Calculate |
| Calculated | Entries/totals generated | Adjust, recalculate, approve |
| Approved | Calculations accepted; attendance locked | Post |
| Posted | Salary balances and advance recovery recognized | Record salary payments |
| Cancelled | Payroll effects reversed and history retained | View only |

# Payroll Entry Payment

| Status | Meaning |
| --- | --- |
| Unpaid | No posted salary payment against the entry |
| Partially Paid | Some salary paid; outstanding remains |
| Paid | Salary payments cover net payable |

# Salary Payments

| Status | Meaning |
| --- | --- |
| Posted | Active salary payment reducing payroll outstanding |
| Cancelled | Payment reversed; payroll outstanding restored |

# Employee Advances

| Status | Meaning |
| --- | --- |
| Open | Advance has outstanding balance |
| Partially Recovered | Payroll has recovered part of the advance |
| Settled | Advance fully recovered |
| Cancelled | Advance cancelled before any recovery |

# Financial Years

| State | Meaning |
| --- | --- |
| Active | Selected as current operational financial-year setup |
| Inactive | Retained historical/alternate year |

Changing the active Financial Year does not rewrite posted document numbers or dates.

# Status Safety Rules

- Draft generally means editable and not financially posted.
- Posted generally means business/stock/balance effects exist.
- Cancelled means retained history plus reversal, not deletion.
- Paid/Partial/Pending describes settlement, not document validity.
- Active/Inactive controls future selection, not historical visibility.
- Approved attendance can enter payroll; Locked attendance cannot be corrected until payroll reversal.
- Completed Site/Work status should be used only when operationally finished.

Continue with the [Glossary](17-glossary.md).
