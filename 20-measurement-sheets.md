# Measurement Sheets

## Purpose

A Measurement Sheet records pipe installation quantities by project/tower, floor, and fixing location. It provides an organized register for checking completed measurements and sharing an Excel or printed copy with a customer.

This version measures **running metres (RMT)**, not square metres, volume, money, or labour hours. It has **no effect on invoices, stock, customer balances, site cash, payroll, or ledgers**. Approval means an internal measurement check, not a customer signature or a financial posting.

## Access and Navigation

Open **Sites & Expenses > Measurement Sheets**. On mobile, use the Measurement Sheets Home tile or **Add > New measurement sheet**. The module works independently of Sites; a tenant can use it without subscribing to Sites.

SYV Cloud must enable the `measurementSheets` feature. The administrator also grants the relevant Measurement Sheets permissions in **Users & Permissions**. Listing, viewing, creating, editing, deleting, approving, cancelling, printing, and exporting are separate permissions. Admin and Manager role defaults include this module; other roles need an explicit grant. Existing explicit permission choices are preserved.

## Important Terms

| Term | Meaning |
| --- | --- |
| RMT | Running metre: a unit of total installed length. |
| mm | Millimetre. Enter every pipe length in millimetres; 1,000 mm = 1 metre. |
| BOQ | Bill of Quantities reference. Enter a reference provided by the project/client, if available. No BOQ master is required. |
| Elevation | A floor or work level, such as 17th Floor, Terrace, or Ground Floor. |
| Fixing location | Reference labels for the start and end of the installed pipe, such as SW-2 and SW-4. |
| Horizontal / vertical | Separate counts and lengths for each installation direction. |

## Header Fields

| Field | Required? | What to enter |
| --- | --- | --- |
| Sheet number | Generated | Assigned when first saved, such as MS/26-27/0001. It cannot be edited. The prefix and next number follow Settings > Sequences > Measurement Sheet. |
| Project / tower | Required | The project/tower this sheet describes. Use one sheet per tower or independently checked work batch. |
| Sheet date | Required | The date of the measurement record. |
| Customer | Optional | An existing customer. Available only with customer lookup access. Search by name. |
| Site | Optional | An existing site. Available only with site lookup access. Selecting a site fills its customer; a mismatched customer is not allowed. |
| Project address | Optional | Location details relevant to this register. |
| Notes | Optional | Overall measurement notes, scope, or observations. |

The linked customer/site names are saved with the sheet, so later master-name changes do not silently rewrite its context. The **company header and logo** are read from current tenant Company Settings each time you print/export.

## Floor / Work Section Fields

| Field | Required? | What to enter |
| --- | --- | --- |
| Floor / elevation | Required | For example, 17th Floor. |
| Work description | Required | For example, Fixing of M.S. Pipe. |
| BOQ no. | Optional | The customer's BOQ/item reference. |

Add another section for another floor or a different work description. **Duplicate floor / section** copies its measurements and leaves elevation blank so you must enter the new label. You can move sections up/down or remove them after confirmation. At least one section must remain.

## Measurement Row Fields

| Field | Required? | What to enter |
| --- | --- | --- |
| Sr. No. | Generated | Sequential within each section, automatically renumbered after moves/removal. |
| From / To | Optional | Fixing references, for example SW-2 / SW-4. |
| Horizontal count | Conditional | Number of equal-length horizontal pipes. Whole number, zero if unused. |
| H. length (mm) | Conditional | Length of each horizontal pipe in millimetres. |
| Vertical count | Conditional | Number of equal-length vertical pipes. Whole number, zero if unused. |
| V. length (mm) | Conditional | Length of each vertical pipe in millimetres. |
| QTY (RMT) | Calculated | Total running metres for this row. |
| Remarks | Optional | Row-specific observations. |

For every row, enter both a positive count and positive length in at least one direction. Unused directions must have count and length both zero. Negative values, fractional pipe counts, and incomplete pairs are rejected. Lengths support up to three decimal places. A row represents pipes with equal length in each direction; use separate rows for different lengths.

```text
Row RMT = (horizontal count x horizontal length mm
           + vertical count x vertical length mm) / 1000
```

Example: 3 horizontal pipes x 2,300 mm = **6.900 RMT**. Adding 2 vertical pipes x 500 mm makes **7.900 RMT**.

Each row is rounded to three decimals. Section and grand totals sum those rounded row quantities. Displayed live totals are checked and recalculated by the backend on save and approval. Do not enter or manually adjust totals.

Use **Add row**, **Duplicate row**, move up/down, or remove row. Removal asks for confirmation. Each section needs at least one row. A sheet supports up to 100 sections and 2,000 rows; split larger projects into separate sheets.

## Daily Workflow

1. Open Measurement Sheets and choose **+**.
2. Enter project/tower and date; optionally link a customer/site.
3. Enter floor, work description, and the pipe measurements.
4. Add/duplicate rows and floors as needed. Check each floor total.
5. Choose **Save draft**. BillFlow assigns a sheet number.
6. Open the saved sheet and review all measurements. Use **Edit draft** for corrections.
7. Choose **Approve sheet**. The confirmation shows the project, row count, and total RMT. Confirm only after checking them.
8. Use **Print / Save PDF** or **Download Excel** to share the complete register.

On mobile the editor stacks fields in two columns. Tap a row heading to expand its fields; the row heading also shows its quantity. Save stays above the mobile navigation. Actions with multiple choices use a three-dot menu.

Leaving an edited form asks whether to discard unsaved changes. Printing/exporting/approving use saved values and are unavailable while edits are unsaved. Save first. If another user changes the same sheet, BillFlow rejects your stale save/approval; reload and review the latest version before retrying.

## Statuses and Corrections

| Status | Allowed actions, subject to permissions |
| --- | --- |
| DRAFT | Edit, delete with confirmation, approve, duplicate, print/export a marked draft copy. |
| APPROVED | View, duplicate, print/export, or cancel with a reason and confirmation. No editing/deletion. |
| CANCELLED | Retained for history. View, duplicate, and print/export a marked cancelled copy. No editing or reapproval. |

To correct an approved sheet, cancel it with a clear reason and duplicate it into a new draft. Correct the replacement and approve it. The new draft has its own number and a reference to the original. Draft deletion is permanent; its deletion event remains in the audit history. Document creation, updates, approval, cancellation, and deletion use the existing audit log with actor/time and old/new data.

## List, Print, and Excel

The list uses server-side search, filtering, sorting, and pagination. Use the date-range picker or common table filters for sheet number, date, project, customer, site, total, and status. Only the current tenant's documents are returned.

Output actions belong to each sheet, not the current list page. Every output contains **all sections and rows** of the selected sheet.

- Excel preserves the 12-column reference structure, merged/grouped headers, floor totals, grand total, numeric quantities, borders, and signature/stamp space. It has frozen headings and A4 landscape fit-to-width printing. It is a snapshot with numeric values, not an editable calculation engine.
- Print repeats grouped column headings when a floor continues to another page. Choose landscape A4 in the print dialog. Company logo, contact details, GSTIN/PAN appear when configured.
- Draft/cancelled copies carry explicit status markings. Signature areas are blank for Prepared by, Checked by, and Authorized by / Stamp.
- Web opens the browser print dialog or downloads `.xlsx`. Allow popups if prompted. Android uses the existing native print/Save as PDF and system file save picker.
- The separate quotation/invoice Print Template selection does not change this specialized measurement register layout.

## Demo and Scope

The demo seeder includes draft Tower B2 and Tower A1 examples: **520.200 RMT** and **802.500 RMT** respectively. Demo seeding is for a dedicated test tenant/database, not production.

This version does not import Excel, calculate rates/taxes, convert measurements into invoices, track area/volume, attach photos, or collect digital signatures. Site linking is informational only.
