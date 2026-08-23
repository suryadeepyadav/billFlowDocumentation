# Site Management

## What Is the Site Management Module?

Site Management brings project/location information, site cash, direct expenses, material movements, work history, and profitability into one site record.

A site belongs to a customer. It can be created manually or from an accepted quotation.

## Why Is It Used?

Use Sites to:

- Track contract value and project lifecycle
- Assign a BillFlow user as site manager
- Maintain opening and transferred site cash
- Post site expenses against available cash
- Issue/return stock material between warehouse and site
- Maintain dated work history
- View site-linked invoices, receipts, purchases, and payments in costing summaries
- Review profit/loss and cash-flow indicators

## Important Terms

- **Site cash**: Operational cash balance controlled by opening cash, fund transfers, and site expenses.
- **Site ledger**: Immutable credit/debit history of that operational cash.
- **Fund transfer**: Company money added to the site's operational cash.
- **Site expense**: Direct expense deducted from the site's operational cash.
- **Material issue**: Stock moved from warehouse to site.
- **Material return**: Stock moved from site back to warehouse.
- **Direct purchase**: Purchase linked to a site and included in site costing.
- **Contract value**: Agreed project value; it is not the same as invoice revenue.
- **Revenue**: Taxable value of posted site-linked invoices, excluding GST.
- **Profit**: Revenue minus material cost, direct purchase cost, and site expenses.

## Site Fields

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Site code | Generated | Nothing | Assigned from the site sequence |
| Site name | Yes | Clear project/location name | Primary site identifier |
| Customer | Yes | Active customer | Site owner/client |
| Site manager | No | Active BillFlow user | Operational responsibility; this selects a User, not an Employee record |
| Contract value | Yes | Zero or positive agreed value | Displayed in costing and reports |
| Opening cash balance | Yes when creating | Zero or positive starting site cash | Immutable starting ledger credit; hidden during edit |
| Status | No; defaults to ACTIVE | DRAFT, ACTIVE, ON_HOLD, COMPLETED, or CANCELLED | Controls lifecycle and posting availability |
| Start date | No on manual site creation | Actual/planned start | Opening ledger date when provided |
| End date | No | Actual/planned end | Lifecycle reference |
| Site address | No | Project address | Location detail |
| City | No | Site city | Location detail |
| State | No | Site state | Location detail; site tax is driven by party settings, not this field |
| Pincode | No | Postal code | Validated when entered |
| Notes | No | Project notes | Internal context |
| Active | No; defaults on | Whether the site is usable | Posting also requires Status ACTIVE |

### Attachments

Site attachments are URL links, not uploaded files in the current form.

| Field | Required | What to enter |
| --- | --- | --- |
| Attachment name | No | Friendly label; if blank, BillFlow derives one from the URL |
| Attachment URL | Yes to add the attachment | Valid `http://` or `https://` URL |

Select the paperclip icon to add the link. Use the close icon on a link to remove it before saving the site.

## Create a Site Manually

1. Open **Sites & Expenses > Sites**.
2. Select the plus icon.
3. Enter Site name and Customer.
4. Confirm Contract value and Opening cash.
5. Choose Status and optional Site manager.
6. Enter dates/address/attachments/notes as available.
7. Save.

BillFlow creates an Opening Balance ledger entry, even when the opening amount is zero.

## Create a Site from a Quotation

An accepted quotation can create a site when no site is already linked. The form pre-fills Contract value from the quotation total and notes the source quotation. Start date is required in this conversion dialog.

See [Quotations](06-quotations.md).

## Site Lifecycle

| Status | Intended use | Can post transfer/expense/material/work entry? |
| --- | --- | --- |
| DRAFT | Setup not ready | No |
| ACTIVE | Live operational site | Yes, when Active switch is also on |
| ON_HOLD | Temporarily paused | No |
| COMPLETED | Work completed | No |
| CANCELLED | Stopped/cancelled | No |

The **Deactivate site** action sets Active off and Status to CANCELLED after confirmation. Reactivate sets the site active again with Status ACTIVE.

Changing status does not erase ledger, stock, expenses, work history, or costing records.

## Open Site Details

Use the View/Open action on a site. The summary shows:

- Customer
- Contract value
- Opening cash
- Available site cash

Tabs are shown according to subscription features and permissions.

# Ledger

## What Does the Ledger Show?

The Site Ledger contains chronological cash entries:

| Entry | Direction | Effect |
| --- | --- | --- |
| Opening balance | CREDIT | Establishes initial cash |
| Fund transfer | CREDIT | Adds company funds |
| Fund transfer reversal | DEBIT | Removes a cancelled transfer |
| Site expense | DEBIT | Uses site cash |
| Site expense reversal | CREDIT | Restores a cancelled expense |

Each entry displays Date, Entry type, Reference, Credit, Debit, and Running balance. Ledger rows are not editable.

Important: customer Receipts and supplier Payments linked to a site appear in site cash-flow/costing summaries, but they do not automatically change the operational Site cash ledger. Site cash is currently controlled only by opening cash, fund transfers, and site expenses.

# Fund Transfers

## Why Is It Used?

Record company funds supplied to the site for local spending.

### Fund Transfer Fields

| Field | Required | What to enter |
| --- | --- | --- |
| Amount | Yes | Positive amount |
| Transfer date | Yes | Date funds were supplied |
| Payment method | No | Active payment method; useful for traceability |
| Reference number | No | Bank/UPI/cheque reference |
| Notes | No | Transfer purpose/context |

Posting the transfer creates a generated Transfer number, a POSTED transfer, a CREDIT ledger entry, and an increase in Site cash.

## Cancel a Fund Transfer

Cancellation posts a DEBIT reversal. It is blocked if Current site cash is lower than the transfer amount, because that indicates the transferred money has already been used.

Enter a meaningful cancellation reason. The original transfer remains with CANCELLED status.

# Site Expenses

## What Is a Site Expense?

A Site Expense records direct local spending and reduces operational Site cash.

### Site Expense Fields

| Field | Required | What to enter |
| --- | --- | --- |
| Expense head | Yes | Active head applicable to site expenses; can be quick-created |
| Amount | Yes | Positive expense amount |
| Expense date | Yes | Date incurred/paid |
| Payment method | No | Cash/bank/UPI/etc.; can be quick-created |
| Vendor | No | Payee/vendor name |
| Bill number | No | Vendor receipt or bill reference |
| Description | No, but recommended | What was purchased/why spent |

Posting is allowed only when the site is active and has sufficient Site cash. It generates an Expense number, creates a DEBIT ledger entry, and reduces Current site cash.

## Cancel a Site Expense

Cancellation changes the expense to CANCELLED, creates a CREDIT reversal ledger entry, and restores the amount to Site cash. The original expense remains in history.

# Site Materials

## What Is It Used For?

Site Materials moves tracked stock between the warehouse and the selected site.

Use:

- **Issue Material to Site** for warehouse to site.
- **Return Material to Warehouse** for site to warehouse.

### Material Header Fields

| Field | Required | What to enter |
| --- | --- | --- |
| Transaction type | Chosen by action | ISSUE or RETURN |
| Transaction date | Yes | Effective movement date |
| Notes | No | Job/use/return context |

### Material Line Fields

At least one line is required.

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Stock item | Yes | Active STOCK item | Service items are not allowed |
| Quantity | Yes | Positive quantity, minimum 0.001 | Moved between locations |
| Unit rate | Yes | Zero or positive rate | Values material cost |
| Value | Calculated | Quantity multiplied by rate | Included in site material costing |

The item Purchase rate pre-fills Unit rate and can be reviewed before posting.

### Availability Rules

- ISSUE requires enough warehouse stock.
- RETURN requires enough quantity currently at the site.
- BillFlow creates paired OUT/IN movements, so total company stock does not change.
- The Site stock table shows item, code, unit, current quantity, and value at the site.

## Cancel a Material Transaction

Cancellation posts the reverse paired movements and sets the transaction to CANCELLED. It can fail if the source of the reversal no longer has enough stock. For example, cancelling an issue requires the material still to be at the site.

# Site Work History

## What Is It Used For?

Work History records day-by-day work performed at a site: what was done, where, when, by how many workers, and with what status.

### Work History Fields

| Field | Required | What to enter | Notes |
| --- | --- | --- | --- |
| Work number | Generated | Nothing | Assigned from work-history sequence |
| Work name | Yes | Activity name | Example: Gate Installation |
| Work status | No; defaults to PENDING | PENDING, IN_PROGRESS, ON_HOLD, or COMPLETED | CANCELLED is set only by cancellation action |
| Location | No | Area within site | Example: Tower A, Main Entrance |
| Work date | Yes | Date of work | Day-by-day history date |
| Number of workers | Yes | Zero or positive whole number | Workforce count, not linked to Employee records |
| Start time | No | Work start time | Needed to calculate duration |
| End time | No | Work end time, later than Start time | Optional; duration shown when both exist |
| Work duration | Calculated | Nothing | Difference between Start and End |
| Completed days | Yes | Zero or positive value; quarter-day increments supported | Progress measure, separate from duration |
| Work details | No | Description of work performed | Operational record |
| Remarks | No | Issues, quality notes, follow-up | Operational record |

Workers in Work History are a numeric count. This feature is independent from Employee Attendance and does not create attendance or payroll entries.

## Edit and Cancel Work History

- Any non-cancelled entry can be edited with Update permission.
- Cancelled entries cannot be edited.
- Cancellation requires a reason and preserves the entry with CANCELLED status.

# Costing

## What Does Site Costing Show?

| Metric | Calculation/meaning |
| --- | --- |
| Invoice revenue | Taxable amount of POSTED invoices linked to the site, excluding GST |
| Material cost | Posted Issue value minus posted Return value, floored at zero |
| Direct purchases | Taxable amount of POSTED purchases linked to the site |
| Site expenses | POSTED site expense amount |
| Total cost | Material cost + Direct purchases + Site expenses |
| Profit / loss | Revenue - Total cost |
| Profit margin | Profit divided by Revenue x 100; zero when Revenue is zero |
| Site cash balance | Current operational Site cash |
| Customer receipts | Total POSTED receipts linked to the site |
| Company fund transfers | Total POSTED site fund transfers |
| Supplier payments | Total POSTED supplier payments linked to the site |
| Material returned | Value of POSTED material returns |

Contract value is displayed as project context but profit uses posted invoice revenue, not Contract value.

Link documents to the correct site at entry time. An unlinked invoice, receipt, purchase, or payment is not included in that site's financial summary.

## Permissions and Feature Controls

- Sites controls site list, details, transfers, lifecycle, and site creation.
- Site Expenses controls expense tab/actions.
- Site Ledger controls ledger visibility.
- Inventory controls material tab/actions.
- Site Work History has its own List, View, Insert, Update, and Cancel permissions and subscription feature.
- Posting additionally requires an Active site with Status ACTIVE.

## Recommended Site Routine

1. Create/activate the site with correct opening cash.
2. Transfer funds before local spending.
3. Record every site expense promptly.
4. Issue and return material through the Materials tab.
5. Add Work History daily.
6. Link invoices, receipts, purchases, and payments to the site where applicable.
7. Review Ledger and Costing weekly.
8. Resolve stock and cash reversals before completing the site.
9. Set Status COMPLETED when no further posting is expected.

## Common Mistakes

- Confusing customer receipts with operational Site cash.
- Entering an incorrect Opening cash amount, which is immutable.
- Posting an expense before transferring enough site cash.
- Linking a financial document to the wrong site.
- Using a stock adjustment instead of Issue/Return for site material.
- Cancelling a transfer after its cash has been spent.
- Cancelling a material issue after the site used/returned the material.
- Treating Work History worker count as Employee Attendance.
- Marking a site Completed or On Hold and then expecting posting actions to remain enabled.

Use [Site P&L, Site Cash Flow, Site Expenses, Site Materials, and Site Ledger reports](14-dashboard-reports-printing-and-exports.md) for broader analysis.
