# Business Masters

## What Is a Master Record?

A master is reusable information selected in later transactions. Examples are customers, suppliers, units, categories, expense heads, and payment methods. Create a master once, then reuse it instead of typing the same information into every document.

Masters are normally deactivated rather than deleted. Deactivation hides them from new-entry dropdowns while preserving historical documents.

## Customers

### What Is This Module?

Customers stores the people and businesses to whom the company sends quotations and invoices and from whom it receives money.

### Why Is It Used?

Customer details drive:

- Quotation and invoice party information
- Receipt allocation and customer outstanding
- Customer-specific sites
- CGST/SGST versus IGST selection through the state code
- Contact details on document previews and prints

### Important Customer Terms

- **Customer name**: Primary searchable/display name.
- **Business name**: Registered or trading business name. Where present, some views prefer it as the party display name.
- **Opening balance**: Amount already owed by the customer when BillFlow begins.
- **Outstanding**: Opening balance plus unpaid posted invoice balances.
- **Credit limit**: Internal reference for desired exposure. The current application stores it but does not automatically block a new invoice when the limit is exceeded.
- **Payment terms days**: Stored reference for the normal terms. The due date is still entered on each invoice in the current workflow.

### Customer Fields

| Field | Required | What to enter | Notes/effect |
| --- | --- | --- | --- |
| Customer name | Yes | Person or organization name | Main identifier |
| Customer type | No; defaults to BUSINESS | INDIVIDUAL or BUSINESS | Classification only |
| Business name | No | Trading/registered business name | Often displayed in party summaries |
| Contact person | No | Main person to contact | Useful for business customers |
| Phone | No | Primary phone | Validated when entered |
| Alternate phone | No | Secondary phone | Validated when entered |
| Email | No | Valid email | Stored in lowercase |
| GSTIN | No | Customer GSTIN | Validated when entered and normalized to uppercase |
| PAN | No | Customer PAN | Validated when entered and normalized to uppercase |
| Credit limit | No; defaults to 0 | Zero or positive reference amount | Informational in the current application |
| Opening balance | No; defaults to 0 | Amount already receivable at migration/start | Adds to customer outstanding |
| Payment terms (days) | No; defaults to 0 | Normal number of credit days | Reference field; enter each invoice due date explicitly |
| Address | No | Billing/contact address | Available to party records |
| City | No | City | Address detail |
| State | No, but important for GST | Full state name | Place-of-supply description |
| State code | No, but important for GST | GST state code | Compared with company state code for tax split |
| Pincode | No | Postal code | Validated when entered |
| Notes | No | Internal customer notes | Not a substitute for document-specific notes |
| Active | No; defaults on | Whether selectable in new transactions | Turn off to deactivate |

### Add a Customer

1. Open **Sales > Customers**.
2. Select the plus icon.
3. Enter Customer name and any available identity/contact fields.
4. Enter State code before creating GST documents.
5. Enter Opening balance only when migrating a verified receivable.
6. Leave Active on.
7. Save.

You can also add a customer from the Customer dropdown in quotation, invoice, receipt, or site entry when you have Insert permission.

### Edit, Deactivate, and Reactivate

- Edit corrects master details used for future selection and display.
- Deactivate after confirming no new transaction should use the customer.
- Historical quotations, invoices, receipts, and sites retain their customer reference.
- Reactivate when the relationship resumes.

Posted documents keep tax and line snapshots; editing the master does not recalculate old documents.

## Suppliers

### What Is This Module?

Suppliers stores vendors from whom the company buys stock items or services and to whom it makes payments.

### Why Is It Used?

Supplier details drive:

- Purchases and supplier invoice reference
- Supplier payment allocation
- Supplier outstanding and advances
- GST tax split through State code
- Direct-to-site purchase attribution

### Important Supplier Terms

- **Opening balance**: Amount already payable to the supplier when BillFlow begins.
- **Purchased amount**: Total value of posted purchases.
- **Paid amount**: Total posted supplier payments.
- **Outstanding**: Positive amount still payable.
- **Advance**: Payment exceeds opening balance plus purchases; BillFlow displays the excess separately.

### Supplier Fields

| Field | Required | What to enter | Notes/effect |
| --- | --- | --- | --- |
| Supplier name | Yes | Vendor/person name | Main identifier |
| Business name | No | Registered/trading business name | Often used as display name |
| Contact person | No | Main supplier contact | Operational reference |
| Phone | No | Primary phone | Validated when entered |
| Alternate phone | No | Secondary phone | Validated when entered |
| Email | No | Valid email | Stored in lowercase |
| GSTIN | No | Supplier GSTIN | Validated and normalized to uppercase |
| PAN | No | Supplier PAN | Validated and normalized to uppercase |
| Opening balance | No; defaults to 0 | Amount already payable at migration/start | Adds to supplier payable |
| Payment terms (days) | No; defaults to 0 | Normal credit days | Reference field; each purchase due date is entered explicitly |
| Address | No | Supplier address | Contact/reference detail |
| City | No | City | Address detail |
| State | No, but important for GST | Full state name | Place-of-supply description |
| State code | No, but important for GST | GST state code | Compared with company state code for CGST/SGST or IGST |
| Pincode | No | Postal code | Validated when entered |
| Notes | No | Internal supplier notes | Reference only |
| Active | No; defaults on | Whether selectable in new purchases/payments | Lifecycle control |

### Add a Supplier

1. Open **Purchasing > Suppliers**.
2. Select the plus icon.
3. Enter Supplier name.
4. Add GSTIN and State code when GST applies.
5. Enter a verified Opening balance if migrating existing payables.
6. Save.

Suppliers can also be added from Purchase and Payment forms when permitted.

## Categories

### What Is It Used For?

Categories group items and services for clearer maintenance and selection. They do not directly post stock or accounting entries.

| Field | Required | What to enter |
| --- | --- | --- |
| Category name | Yes | Meaningful group name, such as Steel, Hardware, Labour, or Fabrication Services |
| Description | No | Scope or usage of the category |
| Active | No; defaults on | Whether available for new item records |

Categories can be created directly from the Category dropdown in the Item form.

## Units

### What Is It Used For?

Units identify how quantities are measured, such as Nos, Kg, Mtr, Sq Ft, or Hours.

| Field | Required | What to enter | Example |
| --- | --- | --- | --- |
| Unit name | Yes | Full unit name | Kilogram |
| Short name | Yes | Compact label | Kg |
| Decimal places | No; defaults to 2 | Zero or positive precision preference | 3 for measurements using 0.001 |
| Active | No; defaults on | Whether available for new items | On |

The selected unit is copied into transaction line snapshots. Changing a unit later does not rewrite old document lines.

Units can be created from the Unit dropdown in the Item form.

## Expense Heads

### What Is It Used For?

Expense heads classify expenses, especially site expenses, so users and reports can understand where money was spent.

| Field | Required | What to enter | Meaning |
| --- | --- | --- | --- |
| Expense head name | Yes | Expense category name | Example: Transport, Labour Food, Fuel |
| Applies to | No; defaults to BOTH | SITE, GENERAL, or BOTH | SITE is site-only; GENERAL is general business; BOTH may be used in either context |
| Description | No | Explanation of included expenses | Helps consistent classification |
| Active | No; defaults on | Whether available for new expenses | Lifecycle control |

The current Site Expense form uses active heads applicable to site activity. Create a missing head directly from that form when permitted.

## Payment Methods

### What Is It Used For?

Payment methods identify how money was received, paid, or transferred. They improve reconciliation and document clarity.

| Field | Required | What to enter | Notes |
| --- | --- | --- | --- |
| Payment method name | Yes | Descriptive name | Example: Cash, HDFC Current Account, UPI Main |
| Type | Yes | CASH, BANK, UPI, CHEQUE, CARD, or OTHER | Broad classification |
| Account name | No | Bank/account holder or wallet name | Useful for non-cash methods |
| Account number | No | Account reference | Store only when operationally appropriate |
| IFSC code | No | Bank IFSC | Normalized/validated where applicable |
| Use as default payment method | No; off by default | Turn on for the normal method | BillFlow keeps one active method as default |
| Active | No; defaults on | Whether available in new forms | Deactivation also removes default status |

The default method is preselected in forms that support it, including new receipts and supplier payments.

## Master Data Quality Checklist

- Avoid duplicate customers or suppliers with slightly different spellings.
- Use consistent unit abbreviations.
- Enter GSTIN/PAN only when verified.
- Enter two-digit GST state codes consistently.
- Do not use Opening balance for a new invoice or purchase; it is for pre-BillFlow balances.
- Keep internal Notes professional and useful.
- Deactivate obsolete records instead of creating historical gaps.

## Related Guides

- [Items and Inventory](05-items-and-inventory.md)
- [Invoices and Receipts](07-invoices-and-receipts.md)
- [Purchases and Payments](08-purchases-and-payments.md)
- [Site Management](09-site-management.md)
