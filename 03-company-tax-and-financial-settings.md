# Company, Tax, Financial Year, and Other Settings

## What Is the Settings Module?

Settings defines the tenant's identity, tax behavior, document numbering, financial years, appearance, and audit visibility. These values affect documents across BillFlow, so administrators should configure them before normal transaction entry.

The available tabs are Company, Tax, Financial years, Sequences, Audit, Appearance, and Subscription.

## Company Settings

### Why Is It Used?

Company settings provide the identity printed on quotations, invoices, receipts, purchases, payments, payroll outputs, and other business documents. The company state information also supports GST configuration.

### Company Fields

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Business name | Yes | The normal trading name | Primary company name in BillFlow and printed documents |
| Legal name | No | Registered legal entity name | Used where a formal name is useful |
| Email | No | Valid company email | Company contact detail |
| Phone | No | Primary company phone | Company contact detail |
| Alternate phone | No | Secondary phone | Additional contact detail |
| Address | No | Registered or operating address | Printed company address |
| City | No | Business city | Address and print output |
| State | No, but important for GST | Full state name | Company location |
| State code | No, but important for GST | Indian GST state code, normally two digits | Compared with customer/supplier state code for tax split |
| Pincode | No | Valid postal code | Company address |
| GSTIN | No unless GST-registered operation requires it | 15-character GST identification number | Printed tax identity; lowercase input is normalized to uppercase |
| PAN | No | 10-character PAN | Printed/legal identity; lowercase input is normalized to uppercase |
| Business type | No | Example: Proprietorship, LLP, Private Limited | Descriptive company classification |

### Company Logo

The logo control accepts PNG, JPEG, or WebP image files. Use a clear image with a sensible aspect ratio and readable content.

1. Choose a file in **Company logo**.
2. Select the upload icon.
3. Confirm that the preview updates.

The current logo appears on supported printed business documents. Uploading a replacement removes the previous tenant logo from storage after the new logo is accepted. Use the delete icon and confirm the dialog to remove the logo.

The maximum image size is validated by the application. If the upload is rejected, use a smaller PNG/JPEG/WebP file.

## Tax Settings

### Why Is It Used?

Tax settings control whether GST is calculated, whether entered rates are inclusive or exclusive, how state tax is split, whether totals are rounded, and what default terms appear on new documents.

Configure these values before the first quotation, invoice, or purchase. Each posted document stores a tax snapshot, so later setting changes do not rewrite old documents.

### Tax Switches

| Field | Required | Meaning |
| --- | --- | --- |
| Tax enabled | No; switch | Master switch for tax calculation |
| GST registered | No; switch | Indicates that the business is GST registered; GST is calculated only when both Tax enabled and GST registered are on |
| Round off | No; switch | Rounds the calculated document total to the nearest whole INR and records the difference as Round Off |

### Tax Fields

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| GSTIN | No | Company GSTIN | Tax identity; normalized to uppercase |
| PAN | No | Company PAN | Tax identity; normalized to uppercase |
| Tax calculation | No; defaults to EXCLUSIVE | EXCLUSIVE or INCLUSIVE | Determines whether line rates exclude or already include GST |
| Default GST % | No; 0 to 100 | Common total GST rate, such as 18 | Used as the default when an item/line does not supply another rate |
| CGST % | No; 0 to 100 | Reference/default CGST component | Saved in tax settings |
| SGST % | No; 0 to 100 | Reference/default SGST component | Saved in tax settings |
| IGST % | No; 0 to 100 | Reference/default IGST component | Saved in tax settings |
| Business state | No, but important | State from which the supply is made | Stored in the document tax snapshot |
| State code | No, but important | Business GST state code | Compared with the customer/supplier state code |
| Default invoice terms | No | Standard payment/legal terms | Pre-fills the Terms field on new sales documents |

### How GST Is Selected

BillFlow uses the **total GST rate on each line** and then chooses the tax type:

- Same non-empty business and party state codes: tax is split equally into CGST and SGST.
- Different non-empty state codes: the complete tax is IGST.
- Missing state code: BillFlow cannot establish an inter-state difference, so it follows the intra-state split. Enter state codes to avoid incorrect tax treatment.
- Tax disabled or GST registered off: CGST, SGST, and IGST are zero.

The current calculation splits an intra-state line's total GST rate equally. The saved CGST, SGST, and IGST default component fields do not replace the line's total GST rate.

### Exclusive Tax Example

For quantity 1, rate INR 1,000, discount 0%, and GST 18%:

- Taxable amount: INR 1,000
- Same-state tax: CGST INR 90 + SGST INR 90
- Inter-state tax: IGST INR 180
- Total before round off: INR 1,180

### Inclusive Tax Example

For an entered line amount of INR 1,180 inclusive of 18% GST:

- Taxable amount: INR 1,000
- Tax component: INR 180
- Total remains INR 1,180 before any round off

### Tax Rate Priority

When a master item is selected, its tax rate pre-fills the line. A user can change the line rate before posting. If no item-specific rate is available, the default GST rate is used.

## Financial Years

### Why Is It Used?

Financial years define the active accounting period and support document numbering. BillFlow can store multiple years, but only one should be active at a time.

### Financial Year Fields

| Field | Required | What to enter |
| --- | --- | --- |
| Label | Yes | Human-readable name, such as `FY 26-27` |
| Code | Yes | Short code used in numbering, such as `26-27` |
| Start date | Yes | First day of the year |
| End date | Yes | Last day; must be after Start date |
| Set active | No; switch | Makes this year active and marks other years inactive |

Use the Set Active action on an existing year to change the workspace year. This does not renumber posted documents and does not reset existing counters by itself.

## Document Sequences

### What Is a Sequence?

A sequence generates unique document identifiers. Examples include quotation numbers, invoice numbers, site codes, employee codes, and payroll numbers.

### Sequence Fields

| Field | Required | Meaning |
| --- | --- | --- |
| Document | Generated/read-only | The sequence type being configured |
| Prefix | Yes | Text before the number, such as `INV` or `QUO` |
| FY code | Yes in the current settings screen | Financial-year segment, such as `26-27` |
| Last number | Yes; zero or positive | Last number already used; the preview shows the next number |
| Padding | Yes; positive integer | Minimum digits in the counter, such as 4 for `0001` |
| Preview | Calculated | Example of the next generated number |

Supported sequence types include quotation, invoice, receipt, payment, purchase, expense, site, fund transfer, material issue, work history, employee, work location, shift, payroll, employee advance, and salary payment.

### Sequence Safety

- Changing Prefix or FY code affects future numbers only.
- Changing Last number can cause confusing gaps or duplicate-number failures if set incorrectly.
- Do not reduce Last number below a number already used.
- Padding changes presentation, not the underlying counter.
- Save each sequence row separately using its save icon.

## Audit Tab

The Audit tab shows recent recorded events with:

- Date and time
- User
- Module
- Action

Use it to identify who created, updated, accepted, approved, cancelled, or otherwise changed audited records. The Settings screen currently loads the latest 25 events. Audit logs are historical records and are not editable from this tab.

## Appearance

### Primary Color

Choose one swatch and select **Save primary color**. The primary color is stored for the tenant and applies after users of that tenant sign in. It affects buttons, active navigation, charts, and other primary accents.

The swatch preview is immediate, but the change is not permanent until saved.

### Color Mode

Choose Light or Dark. Color mode is currently stored as a local browser preference, not as a company-wide backend setting. Different users or browsers can therefore use different modes while sharing the same tenant primary color.

## Subscription Tab

The Subscription tab is read-only in BillFlow. It displays:

- Package name
- Tenant ID
- Active/inactive status
- Product
- Package type
- Expiry date
- Last sync date
- Enabled features
- Package limits

Subscription data is managed by SYV Cloud. See [Users, Permissions, and Subscription](13-users-permissions-and-subscription.md).

## Recommended Setup Review

Before going live, verify:

1. Business and legal names are correct.
2. The company logo prints clearly.
3. Business and party state codes are present.
4. GST registration and Inclusive/Exclusive mode are correct.
5. Default GST and item GST rates are correct.
6. The active financial year is correct.
7. Every sequence preview is unique and uses the intended FY code.
8. Default terms are suitable for customer documents.

## Common Mistakes

- Entering the state name but leaving State code blank, causing an incorrect tax split.
- Treating Inclusive rates as Exclusive or vice versa.
- Changing the active financial year without reviewing sequence FY codes.
- Setting Last number to the next desired number instead of the last already used.
- Uploading a very wide or very small logo that prints poorly.
- Assuming dark mode is shared with every user; it is not.

For GST terms, see [Glossary](17-glossary.md). For correction steps, see [Troubleshooting and FAQ](18-troubleshooting-and-faq.md).
