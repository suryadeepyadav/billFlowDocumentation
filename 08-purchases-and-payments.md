# Purchases and Payments

## Module Overview

Purchases record goods/services received from suppliers. Payments record money paid to suppliers and optionally allocate it against open purchases. Stock items on a posted purchase enter the warehouse or a selected site.

## Important Terms

- **Supplier invoice number**: The vendor's own bill number, separate from BillFlow's generated Purchase number.
- **Receive directly at site**: Posts stock items into the selected site's stock instead of the warehouse.
- **Payment allocation**: Amount assigned to a specific purchase.
- **Supplier advance**: Posted payment amount not currently allocated to purchases, or net payment above payable balance.
- **Purchase balance**: Purchase total minus allocated posted payments.
- **Outstanding**: Positive amount still payable after opening balance, purchases, and payments.

# Purchases

## What Is the Purchase Module?

A purchase is a posted supplier document. It creates a payable and may increase stock.

The current interface posts a purchase immediately. There is no draft/edit stage after posting.

## Purchase Header Fields

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Purchase number | Generated | Nothing | Assigned from purchase sequence |
| Supplier | Yes | Active supplier | Source of GST state code and payable party |
| Receive directly at site | No | Active site, or leave blank | Selected: stock enters site; blank: stock enters warehouse |
| Purchase date | Yes | Supplier transaction/receipt date | Used for stock and reporting |
| Due date | No, but recommended | Expected supplier payment date | Used for overdue payables and aging |
| Supplier invoice number | No, but recommended | Vendor's bill number | Reconciliation and duplicate checking reference |

A missing supplier can be quick-created. The site field is optional and is not restricted by supplier because suppliers are independent of sites.

## Purchase Line Fields

At least one line is required.

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Choose item | No | Existing item/service master | Fills name, purchase rate, tax, unit, and item type |
| Item or service name | Yes | Purchased item/service description | Free text is treated as service and has no stock effect |
| Quantity | Yes | Positive quantity, minimum 0.001 | Used for value and stock |
| Rate | Yes | Zero or positive purchase rate | Defaults from item Purchase rate |
| Discount % | No; defaults to 0 | 0 to 100 | Reduces line before tax |
| GST % | No; defaults from item/settings | Total GST rate, 0 to 100 | Split using company/supplier state codes |
| Amount | Calculated | Nothing | Line total after discount and tax |

You can quick-add an item or service. Select the item master for physical stock; a manually typed line does not affect inventory.

## Notes, Terms, and Totals

| Field/value | Required | Meaning |
| --- | --- | --- |
| Notes | No | Purchase-specific context |
| Terms | No | Supplier terms or internal conditions |
| Subtotal | Calculated | Quantity multiplied by rate before discount |
| Discount | Calculated | Total discount |
| CGST/SGST | Calculated | Same-state GST split |
| IGST | Calculated | Inter-state GST |
| Round off | Calculated | Whole-INR adjustment when enabled |
| Total | Calculated | Total payable for the purchase |

## What Happens When a Purchase Is Posted?

BillFlow:

1. Generates a Purchase number.
2. Stores supplier, line, tax, and terms snapshots.
3. Sets Status to POSTED and Payment status to PENDING.
4. Sets Amount paid to 0 and Balance to the total.
5. Adds the balance to supplier payables.
6. Posts PURCHASE_IN movements for selected stock items.

Stock location:

- No site: warehouse.
- Site selected: that site.

Service and free-text lines do not create stock movement.

## Purchase Statuses

### Document Status

- **POSTED**: Active payable and stock effect.
- **CANCELLED**: Reversed historical purchase.

### Payment Status

- **PENDING**: No active allocated payment.
- **PARTIAL**: Some amount paid.
- **PAID**: Balance zero.

## View Supplier Outstanding

Use Supplier Outstanding from a purchase row. It shows:

- Supplier
- Purchased amount
- Paid amount
- Outstanding
- Open purchase date, due date, balance, and status

At report level, supplier balance is calculated as:

`Opening balance + Posted purchases - Posted payments`

If the result is positive, it is Outstanding. If negative, the absolute amount is Supplier advance.

## Print a Purchase

The formatted print contains company and supplier details, purchase references, site when present, lines, applicable taxes, totals, and terms/notes. Zero-value optional rows are hidden.

## Cancel a Purchase

A purchase can be cancelled only when:

- Status is POSTED.
- Amount paid is zero.
- The original stock can be reversed from its location.
- The user has Cancel permission.

If a supplier payment is allocated to it, cancel that payment first. Cancellation posts PURCHASE_REVERSAL stock OUT at the original warehouse/site location. If the received stock has already been consumed, issued, sold, or returned and is insufficient, cancellation is rejected.

# Supplier Payments

## What Is the Payment Module?

A Payment records money paid to a supplier. It can be allocated to one or more open purchases or stored as unallocated supplier advance.

## Payment Fields

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Payment number | Generated | Nothing | Assigned from payment sequence |
| Supplier | Yes | Active supplier | Loads open purchases |
| Linked site | No | Related site | Attributes payment to site cash-flow/costing context where applicable |
| Payment date | Yes | Date money was paid | Transaction/report date |
| Paid amount | Yes | Positive amount, minimum 0.01 | Total supplier payment |
| Payment method | No | Active payment method | Default method is preselected when configured |
| Reference number | No | UTR, cheque, bank reference, etc. | Reconciliation aid |
| Notes | No | Payment context | Internal/document note |

A missing supplier or payment method can be quick-created when permitted.

## Purchase Allocation

After choosing a supplier, BillFlow loads that supplier's open purchases.

| Column | Meaning |
| --- | --- |
| Purchase | BillFlow purchase number |
| Date | Purchase date |
| Balance | Current open amount |
| Allocate | Amount of this payment to assign |

Rules:

- Each allocation must be positive to be included.
- It cannot exceed the purchase balance.
- Total allocations cannot exceed Paid amount.
- One payment may cover multiple purchases.
- Allocation is optional.

The form displays Paid, Allocated, and Unallocated.

## Supplier Advance and Later Allocation

If a posted Payment has Unallocated amount greater than zero, use **Allocate supplier advance** from its row actions:

1. Open the action.
2. Review Available advance.
3. Enter amounts against current open purchases.
4. Ensure total Allocating does not exceed Remaining advance or purchase balances.
5. Select **Allocate advance**.

This updates purchase balances while preserving the original payment amount and payment date.

## What Happens When a Payment Is Posted?

BillFlow:

1. Generates the payment number.
2. Sets Status to POSTED.
3. Applies allocations to purchases.
4. Recalculates each purchase's Amount paid, Balance, and Payment status.
5. Stores any remainder as Unallocated amount.
6. Reduces the supplier's net payable balance.

## Cancel a Payment

A POSTED payment can be cancelled with Cancel permission.

Cancellation:

- Changes status to CANCELLED.
- Reverses every allocation made by that payment, including later advance allocations.
- Restores purchase balances and payment statuses.
- Removes the payment from active supplier payable calculations.
- Preserves transaction and cancellation history.

If one payment covers multiple purchases, all of its allocations are reversed together.

## Allocation Examples

### Exact Payment

Purchase balance INR 25,000, payment INR 25,000, allocation INR 25,000:

- Purchase becomes PAID.
- Payment Unallocated is INR 0.

### Partial Payment

Purchase balance INR 25,000, payment/allocation INR 10,000:

- Purchase becomes PARTIAL.
- Purchase Balance becomes INR 15,000.

### Advance

Payment INR 30,000, current allocation INR 20,000:

- Unallocated supplier advance: INR 10,000.
- The INR 10,000 can be allocated later to another purchase.

## Permissions

Purchases and Payments use separate modules and permissions:

| Action | Typical permission |
| --- | --- |
| List | List |
| Preview/outstanding | View |
| Post purchase/payment | Insert |
| Allocate existing supplier advance | Update on Payments |
| Cancel | Cancel |
| Print | Print |
| Export list | Export where enabled |

Inventory and Site behavior also requires the related licensed features where those screens/actions are used.

## Recommended Procure-to-Pay Workflow

1. Verify/create supplier and GST state code.
2. Verify item masters and purchase rates.
3. Post purchase at Warehouse or the correct Site.
4. Confirm stock movement and purchase balance.
5. Record the payment with actual method/reference.
6. Allocate to purchases.
7. Allocate any prior supplier advance where appropriate.
8. Review Supplier Outstanding and reports.

## Common Mistakes

- Leaving Site blank when material was received directly at a site.
- Selecting Site for a warehouse delivery.
- Entering stock as free text and expecting inventory to increase.
- Leaving Due date blank and losing overdue reporting value.
- Posting payment without allocation when it should settle a purchase.
- Cancelling a purchase after the stock has left its original location.
- Trying to cancel a purchase before cancelling allocated payments.

See [Items and Inventory](05-items-and-inventory.md), [Site Management](09-site-management.md), and [Status Reference](16-status-reference.md).
