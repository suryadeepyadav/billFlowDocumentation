# Invoices and Receipts

## Module Overview

Sales Invoices record amounts billed to customers. Receipts record money received and optionally allocate it against open invoices. Together they maintain invoice payment status, customer receivables, and customer transaction history.

## Important Terms

- **Posted**: The document is final and has affected balances; an invoice may also affect stock.
- **Pending/Unpaid**: No receipt amount has been allocated to the invoice.
- **Partial**: Some, but not all, of the invoice has been paid.
- **Paid**: Invoice balance is zero.
- **Allocation**: Part of a receipt assigned to a specific invoice.
- **Unallocated amount**: Receipt money not assigned to an invoice; recorded as customer advance.
- **Amount paid**: Sum of active receipt allocations against the invoice.
- **Balance amount**: Invoice total minus Amount paid.
- **Outstanding**: Customer opening balance plus current posted invoice balances.
- **Due date**: Expected payment date, used for overdue and aging information.

# Sales Invoices

## What Is the Invoice Module?

An invoice is a posted customer sales document. It creates a receivable and, for selected stock items, removes quantity from warehouse stock.

Unlike quotations, invoices are posted immediately when saved. The current interface does not provide a draft or edit stage for an invoice.

## Ways to Create an Invoice

### Direct Invoice

Open **Sales > Sales Invoices**, select the plus icon, and enter the transaction.

### From an Accepted Quotation

Use **Create invoice** on an accepted quotation. BillFlow opens the invoice form with the customer, site, quotation link, lines, notes, and terms prefilled. Review every value before posting.

## Invoice Header Fields

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Invoice number | Generated | Nothing | Assigned from the invoice sequence |
| Customer | Yes | Active customer | Party billed and source of GST state code |
| Linked site | No | Active site belonging to the selected customer | Attributes invoice revenue to site costing/reporting |
| Invoice date | Yes | Billing date | Used in financial/report periods |
| Due date | No, but recommended | Expected payment date | Drives overdue alerts and aging |
| Quotation reference | Generated when converted | Nothing | Links the invoice to its accepted quotation |

Customer and site are chosen before posting. A missing customer can be quick-created when the user has permission.

## Invoice Line Fields

At least one line is required.

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Choose item | No | Existing item/service master | Fills the line defaults and determines stock behavior |
| Item or service name | Yes | Customer-facing line name | A free-text line is treated as a service |
| Quantity | Yes | Positive quantity, minimum 0.001 | Used for value and stock quantity |
| Rate | Yes | Zero or positive selling rate | Defaults from item Sale rate |
| Discount % | No; defaults to 0 | 0 to 100 | Reduces taxable value before GST |
| GST % | No; defaults from item/settings | Total GST rate from 0 to 100 | Split according to state codes |
| Amount | Calculated | Nothing | Final line total after discount and tax |

Use the plus icon to add lines and the minus icon to remove them. At least one line must remain.

## Invoice Notes, Terms, and Totals

| Field/value | Required | Meaning |
| --- | --- | --- |
| Notes | No | Invoice-specific context |
| Terms | No | Payment/legal terms; defaults from Tax Settings |
| Subtotal | Calculated | Quantity multiplied by rate before discount |
| Discount | Calculated | Total discount |
| CGST/SGST | Calculated | Same-state tax components |
| IGST | Calculated | Inter-state tax component |
| Round off | Calculated | Whole-INR adjustment when enabled |
| Total | Calculated | Amount billed |

## What Happens When an Invoice Is Posted?

BillFlow:

1. Generates the invoice number.
2. Stores party, line, tax, and terms snapshots.
3. Sets document Status to POSTED.
4. Sets Payment status to PENDING.
5. Sets Amount paid to 0 and Balance to the invoice total.
6. Adds the balance to customer receivables.
7. Creates SALE_OUT movements for selected STOCK items.

Invoice stock always leaves the warehouse in the current implementation, even when the invoice is linked to a site. Site linkage is used for project financial attribution, not as the invoice stock source.

Posting is rejected if warehouse stock is insufficient for one or more selected stock items.

## Invoice Statuses

### Document Status

- **POSTED**: Active invoice affecting receivables and stock.
- **CANCELLED**: Reversed invoice retained in history.

### Payment Status

- **PENDING**: No active receipt allocation.
- **PARTIAL**: Amount paid is greater than zero but less than total.
- **PAID**: Balance is zero.

Payment status is calculated from active allocations. Do not edit it manually.

## View Customer Outstanding

Use the Customer Outstanding action on an invoice to see:

- Customer
- Total invoiced
- Total allocated/received against invoices
- Outstanding
- Open invoice number, date, due date, balance, and payment status

The outstanding amount includes the customer's Opening balance plus open posted invoice balances.

Important current behavior:

- Unallocated receipt advances are tracked on receipts and reports but are not automatically subtracted from the Customer Outstanding dialog.
- Receipt allocation supports posted invoices, not a separate opening-balance settlement row.
- Plan migrated opening balances carefully and allocate incoming receipts to invoices whenever possible.

## Print an Invoice

Use Print to open the formatted invoice. It includes company logo/details, customer, date, line details, applicable taxes, total, notes, and terms. Optional zero-value Discount, CGST, SGST, IGST, and Round Off rows are hidden.

Use the browser print dialog to print or save as PDF.

## Cancel an Invoice

An invoice can be cancelled only when:

- Its document status is POSTED.
- Amount paid is zero.
- The user has Cancel permission.

If a receipt is allocated, cancel that receipt first. Then cancel the invoice.

Cancellation:

- Changes status to CANCELLED.
- Removes its active receivable effect.
- Posts SALE_REVERSAL stock IN movements for its stock lines.
- Preserves the invoice and cancellation audit details.

The invoice cannot be edited after cancellation.

# Receipts

## What Is the Receipt Module?

A receipt records money received from a customer. It may be allocated to one or more open invoices during entry.

## Receipt Fields

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Receipt number | Generated | Nothing | Assigned from the receipt sequence |
| Customer | Yes | Active customer | Determines available open invoices and sites |
| Linked site | No | Site belonging to the customer | Attributes the receipt to a site for cash-flow reporting |
| Receipt date | Yes | Date money was received | Transaction/report date |
| Received amount | Yes | Positive amount, minimum 0.01 | Total money recorded |
| Payment method | No | Cash, bank, UPI, cheque, card, or other method | Default method is preselected when configured |
| Reference number | No | Bank reference, UTR, cheque number, etc. | Reconciliation aid |
| Notes | No | Receipt context | Internal/document note |

A missing customer or payment method can be quick-created when permitted.

## Invoice Allocation Fields

After selecting a customer, BillFlow loads that customer's open invoices.

| Column | Meaning |
| --- | --- |
| Invoice | Open invoice number |
| Date | Invoice date |
| Balance | Maximum currently payable balance |
| Allocate | Amount of this receipt to apply to the invoice |

Rules:

- Each allocation must be zero or positive.
- An allocation cannot exceed the invoice balance.
- Total allocations cannot exceed Received amount.
- One receipt can be split across multiple invoices.
- Allocation is optional.

The summary shows:

- **Received**: Total receipt amount.
- **Allocated**: Sum assigned to invoices.
- **Unallocated**: Received minus Allocated.

## Allocation Examples

### Full Payment

Invoice balance INR 10,000, receipt INR 10,000, allocation INR 10,000:

- Receipt allocated: INR 10,000
- Receipt unallocated: INR 0
- Invoice payment status: PAID

### Partial Payment

Invoice balance INR 10,000, receipt INR 4,000, allocation INR 4,000:

- Invoice amount paid increases by INR 4,000
- Invoice balance becomes INR 6,000
- Invoice payment status becomes PARTIAL

### Customer Advance

Receipt INR 12,000, allocations INR 10,000:

- Allocated: INR 10,000
- Unallocated customer advance: INR 2,000

The current Receipt list does not provide a later **Allocate advance** action. To ensure a payment reduces an invoice, allocate it during receipt entry. If a posted receipt was allocated incorrectly, the safe current correction is normally to cancel it and post the corrected receipt, subject to company policy and permissions.

## What Happens When a Receipt Is Posted?

BillFlow:

1. Generates the receipt number.
2. Sets receipt Status to POSTED.
3. Applies each allocation to the target invoice.
4. Recalculates invoice Amount paid, Balance, and Payment status.
5. Stores any remainder as Unallocated amount.
6. Updates customer and site-related reporting where applicable.

## Print a Receipt

The receipt print shows company, customer, receipt amount, allocations, applicable unallocated amount, payment context, and notes. Zero-value optional rows are omitted.

## Cancel a Receipt

A POSTED receipt can be cancelled with Cancel permission.

Cancellation:

- Changes receipt Status to CANCELLED.
- Reverses all of that receipt's invoice allocations.
- Restores invoice balances and recalculates payment statuses.
- Preserves the receipt and cancellation history.

If one receipt was split across several invoices, cancelling it reverses every allocation in that receipt.

## Permissions

Invoices and Receipts have separate feature and permission checks. Typical actions use:

| Action | Permission |
| --- | --- |
| List | List |
| Preview/detail | View |
| Post new document | Insert |
| Cancel | Cancel |
| Print business document | Print |
| Export list | Export where enabled |

Quick Add also requires Insert permission for the relevant master.

## Recommended Daily Sales Collection Workflow

1. Review open/overdue invoices.
2. Confirm the customer and actual money received.
3. Select the correct payment method and reference.
4. Allocate against specific invoices.
5. Verify Unallocated before posting.
6. Print/send the receipt if required.
7. Recheck Customer Outstanding.

## Common Mistakes

- Posting an invoice before checking stock.
- Leaving Due date blank and losing useful aging/overdue information.
- Entering a customer state code incorrectly and getting the wrong GST split.
- Recording a receipt but leaving allocations blank when it should pay an invoice.
- Allocating more than the receipt or invoice balance.
- Trying to cancel an invoice before cancelling allocated receipts.
- Assuming a site-linked invoice consumes site stock; it consumes warehouse stock.

See [Status Reference](16-status-reference.md) and [Troubleshooting and FAQ](18-troubleshooting-and-faq.md) for quick checks.
