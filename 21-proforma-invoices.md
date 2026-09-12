# Proforma Invoices and Progressive RA Billing

## What Is This Module?

The Proforma Invoices module prepares commercial billing documents before an accounting Sales Invoice is posted. It supports:

- **Standard Proforma** for ordinary item/service proposals with invoice-style GST and totals.
- **Progressive / RA Proforma** for claiming measured work against an approved work order over multiple billing periods.

Proforma Invoices are separate from Sales Invoices. A Proforma Invoice does not itself create revenue, customer outstanding, stock movement, GST-report entries, site costing revenue, or ledger entries.

## Why Is It Used?

Use a Standard Proforma when the customer needs invoice-like commercial details before the final invoice is raised. Use a Progressive / RA Proforma when work is billed in stages and every claim must show:

- Work-order quantity and value.
- Quantity and amount billed previously.
- Quantity and amount claimed now.
- Cumulative quantity and amount after the current claim.

After the customer approves an issued Proforma, convert it into an editable Sales Invoice draft. Review and post that Invoice through the normal Sales workflow.

## Access and Placement

Open **Sales > Proforma Invoices**. The module contains two tabs:

- **Proforma invoices**: Standard and RA documents.
- **Work orders**: Approved commercial quantities, units, rates, and GST rates used by RA billing.

The menu requires the tenant feature `proformaInvoices` and suitable Proforma permissions. Measurement import additionally requires the `measurementSheets` feature and Measurement Sheets View permission. Conversion also requires the `invoices` feature and Invoice Insert permission.

## Important Terms

| Term | Meaning |
| --- | --- |
| Proforma Invoice | A non-accounting commercial document issued before a Sales Invoice |
| Standard Proforma | Item/service document calculated like an Invoice but without accounting effect |
| RA | Running Account or progressive bill against a work order |
| Work Order | The customer-approved work, quantity, unit, rate, and GST basis for RA claims |
| Approved Quantity | Maximum claimable quantity on a work-order line |
| Previous | Total of earlier issued, non-cancelled RA current claims |
| Current | Quantity and amount claimed in this RA document |
| Total / Cumulative | Previous plus Current |
| Remaining | Approved work-order quantity minus cumulative billed quantity |
| Measurement Claim | An approved Measurement Sheet reserved by an issued RA document |
| Variation Line | A new work-order line used when a later rate/unit differs from an existing billed line |

## Statuses

| Status | Meaning | Available actions |
| --- | --- | --- |
| DRAFT | Internal preparation with no accounting effect | Edit, duplicate, print, export, issue, cancel, or delete |
| ISSUED | Commercial and tax snapshots are locked | Print, export, convert, duplicate, or cancel when allowed |
| CONVERTED | A linked Sales Invoice draft has been created | View, print, export, or open the linked Invoice |
| CANCELLED | Retained history that is no longer effective | View, print, export, or duplicate |

Issuing requires confirmation. Conversion is idempotent: repeating it returns the existing linked Invoice instead of creating a second one.

## Standard Proforma Fields

| Field | Requirement | What to enter |
| --- | --- | --- |
| Proforma type | Required | Select **Standard Proforma** |
| Accepted quotation | Optional | Select an accepted Quotation to copy its customer, site, and lines |
| Customer | Required | Customer receiving the Proforma |
| Site | Optional | Related customer site/project |
| Proforma date | Required | Commercial document date |
| Valid until | Optional | Last date for which the offer is valid |
| External reference | Optional | Customer enquiry, purchase reference, or other external number |
| Item / service | Optional per line | Existing active Item/Service master |
| Item name | Required per line | Printed line name; filled from the selected master when available |
| Description | Optional | Scope or specification |
| HSN/SAC | Optional | GST classification |
| Unit | Optional | NOS, KG, RMT, SQM, JOB, etc. |
| Quantity | Required | Positive commercial quantity |
| Rate | Required | Non-negative unit rate |
| Discount % | Optional | Line discount from 0 to 100 |
| GST % | Conditional | GST rate when GST is enabled |
| Terms | Optional | Commercial/payment conditions |
| Notes | Optional | Internal or printed supporting notes |

All line values, discounts, tax split, totals, and round-off are recalculated by the backend. Values supplied by the browser are never trusted as final totals.

## Work Order Fields

Create a Work Order before preparing an RA Proforma.

| Field | Requirement | What to enter |
| --- | --- | --- |
| Work-order number | Required | Number from the customer's work order |
| Work-order date | Required | Date on the customer work order |
| External reference | Optional | Tender, contract, or internal reference |
| Customer | Required | Customer that awarded the work |
| Site | Optional | Related BillFlow site for that customer |
| Project | Required | Project/work name |
| Tower | Optional | Tower, block, wing, or section |
| Project address | Optional | Location printed on RA documents |
| Work name | Required per line | Billable work description |
| Item / service | Optional per line | Existing Item/Service reference |
| HSN/SAC | Optional | GST classification |
| Unit | Required | Quantity unit such as SQM or RMT |
| Approved qty | Required | Maximum customer-approved quantity |
| Rate | Required | Agreed unit rate |
| GST % | Optional | Applicable GST rate |
| Description | Optional | Detailed scope |
| Notes | Optional | General work-order notes |

Before the first RA is issued, the Work Order can be edited normally. After billing starts, existing billed lines have locked identity, unit, rate, and tax rate.

## Work Order Amendments

Use **Amend work order** after an RA has been issued. An amendment reason is required and written to the audit log.

- Approved quantity may be increased.
- Approved quantity cannot be reduced below the quantity already billed.
- Existing billed lines cannot be removed.
- Existing billed line item, name, unit, rate, or GST rate cannot be rewritten.
- Add a new variation line when the rate, unit, or commercial identity changes.

These rules keep earlier RA documents and cumulative figures reproducible.

## Creating a Progressive / RA Proforma

1. Open **Proforma Invoices > Work orders**.
2. Create or select the applicable Work Order.
3. Choose **Create RA Proforma**.
4. Review Previous and Remaining quantities for every line.
5. Import compatible approved Measurement Sheets and/or enter a manual Current quantity.
6. Enter a reason for every manual quantity.
7. Save the draft and review the calculated Current and Total values.
8. Confirm **Issue** when the claim is ready.

The user enters only the Current claim. BillFlow calculates Previous, Total, Remaining, taxable amounts, GST, and current/cumulative totals.

## Measurement Sheet Import

Only approved, unclaimed Measurement Sheets are offered.

- Tenant must match.
- Customer must match when the Measurement Sheet has a customer.
- Site must match when the Measurement Sheet has a site.
- Quantity unit must match the Work Order line, for example SQM to SQM or RMT to RMT.
- The complete approved sheet quantity is imported and remains read-only.
- Extra manual quantity must be entered separately with a reason.

Selecting a Measurement Sheet in a draft does not reserve it. Issuing the RA atomically claims it. This allows users to discard or revise drafts without blocking a valid sheet. Cancelling the latest eligible RA releases its claims.

## RA Numbering and Cancellation

Each Work Order receives its own RA series: RA1, RA2, RA3, and so on. Cancelled numbers are not reused.

An issued RA may be cancelled only when it is the latest unconverted RA for that Work Order. A prior RA cannot be cancelled while later issued or converted RAs depend on its Previous values. Cancel later documents first when the business situation permits it.

Converted Proformas cannot be cancelled because a linked Invoice already exists.

## Converting to a Sales Invoice

1. Open an issued Proforma.
2. Select **Convert to invoice**.
3. Confirm creation of the Invoice draft.
4. Open **Sales Invoices** and review the draft.
5. Edit the draft where necessary.
6. Confirm **Post** only after all commercial and tax details are correct.

For a Standard Proforma, all current lines are copied. For an RA Proforma, only the Current claim is copied; Previous and cumulative quantities are not invoiced again.

Editing the converted Invoice draft does not rewrite the issued Proforma. Posting the Invoice is the only step that affects customer outstanding, stock, GST reports, site revenue, and related ledgers.

## Print and Excel

Standard Proformas use the tenant's saved Proforma template under **Settings > Print templates**: Classic, Compact GST, or Modern Branded. Missing settings use Classic.

RA Proformas always use the dedicated landscape progressive layout with:

- Company, customer, work order, project, tower, and RA details.
- Work-order quantity/rate/value.
- Previous, Current, and Total bill quantities.
- Previous, Current, and Total taxable/GST totals.
- Current claim amount in words.
- Bank details, terms, notes, and authorization/stamp area.

Excel export retains numeric amount and quantity cells, merged headings, repeating headers, and landscape print settings. Browser and Android output use BillFlow's existing print/download sharing adapters.

Draft and cancelled outputs have clear watermarks. Issued outputs state that they are Proforma Invoices with no accounting effect.

## Company Bank Details

Configure optional bank details under **Settings > Company**:

- Bank name
- Branch
- Account holder name
- Account number
- IFSC code

BillFlow snapshots these details when a Proforma is issued. Later company-setting changes do not silently rewrite an already issued commercial copy.

## Permissions

The `proformaInvoices` module supports List, Insert, View, Update, Delete, Print, Export, Approve, and Cancel permissions.

- **Approve** controls issuing Proformas and audited Work Order amendments.
- **Delete** applies only to drafts.
- **Cancel** applies only to eligible Draft/Issued documents.
- **Print** and **Export** are independent.
- Invoice Insert permission is also required to convert.

## Common Problems

| Problem | Check |
| --- | --- |
| Proforma menu is missing | SYV Cloud feature `proformaInvoices`, license sync, and user View permission |
| Quotation is unavailable | It must be Accepted and the user needs Quotation View access |
| Measurement Sheet is unavailable | It must be Approved, unclaimed, unit-compatible, and match customer/site |
| Issue is blocked | Current quantity, work-order maximum, stale version, or another user's measurement claim |
| Work Order rate cannot be changed | Billing has started; add a variation line through an amendment |
| Earlier RA cannot be cancelled | A later issued/converted RA depends on it |
| Convert is unavailable | Proforma must be Issued and the user needs Invoice Insert permission |
| No bank details print | Complete Bank details under Company settings before issue |

## Safe Practice Checklist

1. Confirm Customer, Site, Work Order, unit, rate, GST rate, and Current quantity before issue.
2. Use approved Measurement Sheets wherever they are the certified quantity source.
3. Use a clear reason for manual quantity adjustments and Work Order amendments.
4. Never treat an issued Proforma as a posted accounting Invoice.
5. Review the converted Invoice draft before posting.
6. Use cancellation rules instead of trying to rewrite cumulative RA history.
