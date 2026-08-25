# Quotations

## What Is the Quotation Module?

A quotation is a customer proposal containing items/services, prices, discounts, GST, terms, and validity. It is not an invoice and does not create customer receivables or stock movements.

## Why Is It Used?

Use quotations to:

- Prepare a commercial offer before billing
- Track Draft, Sent, and Accepted proposals
- Print or save a professional proposal as PDF
- Create a site after customer acceptance
- Start an invoice from accepted commercial details
- Preserve quoted values and tax calculations for reference

## Important Terms

- **Draft**: Still being prepared; editable.
- **Sent**: Presented to the customer; still editable but eligible for acceptance.
- **Accepted**: Customer-approved; commercial details are locked.
- **Valid until**: Last date the offer is intended to remain valid.
- **Tax snapshot**: Company/party state and tax mode stored with the quotation.
- **Linked site**: Existing customer site associated with the proposal.

## Create a Quotation

1. Open **Sales > Quotations**.
2. Select the plus icon.
3. Choose or quick-add the customer.
4. Optionally select one of that customer's sites.
5. Enter dates and choose Draft or Sent.
6. Add at least one valid line.
7. Review totals, notes, and terms.
8. Select **Save quotation**.

## Quotation Header Fields

| Field | Required | What to enter | Notes/effect |
| --- | --- | --- | --- |
| Quotation number | Generated | Nothing | Created from the quotation sequence |
| Customer | Yes | Active customer | Cannot be changed after the quotation is first saved |
| Linked site | No | Existing active site belonging to the customer | Narrows project attribution; list changes with customer |
| Quotation date | Yes | Proposal date | Defaults to today |
| Valid until | No | Offer expiry date | Used by dashboard expiring-quotation alerts |
| Status | No; defaults to DRAFT | DRAFT or SENT | Only SENT can be accepted |

The Add Customer action is available from the Customer dropdown when the user can create customers.

## Line Fields

At least one line is required.

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Choose item | No | Existing item/service master | Fills name, description, unit, sale rate, and tax rate |
| Item or service name | Yes | Description shown to customer | Can be entered manually |
| Quantity | Yes | Positive quantity, minimum 0.001 | Multiplied by Rate |
| Rate | Yes | Zero or positive unit price | Uses item Sale rate when selected |
| Discount % | No; defaults to 0 | 0 to 100 | Reduces the line before GST calculation |
| GST % | No; defaults from item/settings | 0 to 100 total GST rate | Split into CGST/SGST or IGST |
| Amount | Calculated | Nothing | Taxable amount plus tax after discount |

Use the plus icon above the lines to add another row. Use the minus icon to remove a row. At least one row must remain.

You can quick-add an item. A manually typed line with no valid item master is treated as a service for downstream documents and does not create stock movement.

## Notes, Terms, and Totals

| Field/value | Required | Meaning |
| --- | --- | --- |
| Notes | No | Quotation-specific message or internal/commercial context |
| Terms | No | Commercial/payment/legal terms; pre-filled from Default invoice terms when available |
| Subtotal | Calculated | Quantity multiplied by rate before discounts |
| Discount | Calculated | Total line discounts |
| CGST | Calculated | Same-state central tax |
| SGST | Calculated | Same-state state tax |
| IGST | Calculated | Inter-state integrated tax |
| Round off | Calculated | Nearest-whole adjustment when enabled |
| Total | Calculated | Final quotation amount |

The creation screen shows all totals for verification. Printed output hides optional zero-value tax, discount, and round-off rows.

## GST Behavior

BillFlow compares the company State code from Tax Settings with the customer's State code:

- Same codes: CGST and SGST.
- Different codes: IGST.
- Missing codes: inter-state status cannot be established reliably; complete both master records first.

For Inclusive versus Exclusive calculations, see [Company, Tax, Financial Year, and Other Settings](03-company-tax-and-financial-settings.md).

## Quotation Status Workflow

### Draft

- Editable
- Printable
- Can be cancelled
- Cannot be accepted directly

Change Status to **SENT** and save after the proposal has been shared with the customer.

### Sent

- Editable
- Printable
- Can be accepted with confirmation
- Can be cancelled

Acceptance asks for confirmation because it permanently locks commercial details.

### Accepted

- Cannot be edited
- Can create a Site when no site is linked
- Can create an Invoice
- Can be cancelled only when no site and no invoice has been linked

The accepted quotation remains a historical source record even after site/invoice creation.

### Rejected

The data model recognizes Rejected quotations, and such a record is editable/cancellable if present. The current quotation form exposes Draft and Sent as the user-selectable statuses and does not provide a dedicated Reject action.

### Cancelled

- Remains in history
- Cannot be edited, accepted, or converted
- Stores cancellation date, user, and reason

## Edit a Quotation

The Edit action is available for Draft, Sent, and Rejected records when the user has Update permission.

The customer is locked after creation. Other editable details can be changed and totals are recalculated. Posted invoices or sites created from an accepted quotation are not rewritten by later master changes.

## Accept a Quotation

1. Ensure the quotation is Sent.
2. Review customer, lines, rates, tax, total, validity, and terms.
3. Select **Accept quotation**.
4. Read the lock warning.
5. Confirm.

Acceptance should represent an actual customer decision. Do not use it merely as a print status, because the quotation becomes non-editable.

## Create a Site from an Accepted Quotation

The Create Site action is available when Sites is licensed, the user has permission, the quotation is Accepted, and it has no linked site.

| Field | Required | What to enter |
| --- | --- | --- |
| Site name | Yes | Project/site name; defaults from the customer display name |
| Contract value | Yes | Zero or positive contract value; defaults to quotation total |
| Site manager | No | Existing BillFlow user |
| Opening site cash | Yes | Zero or positive starting site cash |
| Start date | Yes | Planned/actual start date |
| End date | No | Planned/actual completion date |
| Notes | No | Defaults with the source quotation reference |

Creating the site links it to the customer and quotation. See [Site Management](09-site-management.md).

## Create an Invoice from an Accepted Quotation

Select **Create invoice** to open Sales Invoices with:

- Customer preselected
- Linked site copied
- Quotation reference copied
- Lines and values copied for review
- Notes and terms copied

Submitting the invoice form saves an editable Draft. Review it, then use the confirmed Post action; stock is checked at posting, not when the quotation is accepted or the Draft is saved.

See [Invoices and Receipts](07-invoices-and-receipts.md).

## Print a Quotation

Use the Print action to open the formatted document. The print includes company identity/logo, customer, quotation details, lines, applicable tax totals, notes, and terms. Use the browser print dialog to print or save as PDF.

A Draft quotation prints with a prominent `DRAFT` watermark and **DRAFT QUOTATION - NOT FINAL** notice. A Cancelled quotation prints with a `CANCELLED` watermark. Sent and Accepted quotation copies keep the normal clean layout.

Allow pop-ups for BillFlow if the print window does not open.

## Cancel a Quotation

Cancellation uses a confirmation dialog and optional reason field. Enter a meaningful reason even when the field is not technically required.

Cancellation is available for Draft, Sent, and Rejected quotations. An Accepted quotation can be cancelled only if it has no linked site and no invoice created from it.

## Permissions and Subscription

| Action | Typical required permission |
| --- | --- |
| See quotation list | List |
| Open quotation | View |
| Create | Insert |
| Edit | Update |
| Accept | Approve |
| Cancel | Cancel |
| Print | Print |
| Export list | Export where enabled |
| Create customer/item inline | Insert on the corresponding master |

Quotations must also be enabled in the tenant package. Site and Invoice conversion actions require those separate features and permissions.

## Common Mistakes

- Accepting a quotation before final review.
- Leaving it Draft and wondering why Accept is disabled.
- Missing customer State code and getting the wrong GST split.
- Expecting a quotation to reserve or remove stock.
- Typing a stock item manually instead of selecting its master, then expecting stock effects after invoice conversion.
- Creating a site before confirming opening cash and contract value.
- Trying to cancel an accepted quotation after it has a site or invoice.

For every status and next action, see [Status Reference](16-status-reference.md).
