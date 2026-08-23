# Customer and Supplier Statements

## What Is This Feature?

Every Customer and Supplier has a financial dashboard and statement page. It provides a current account position, a selected financial-year/date-range view, source document history, and a chronological debit/credit ledger with running balance.

The balance is calculated from posted transactions. It is not entered or edited manually.

## Open a Statement

1. Open **Customers** or **Suppliers**.
2. Review the new balance column in the list.
3. Open the row Actions menu.
4. Select **Customer dashboard** or **Supplier dashboard**.

The dashboard action requires View permission for the relevant Customer or Supplier module. Print and CSV export require that module's Print or Export permission.

## Current Balance in the List

### Customer

```text
Customer current balance = Opening balance + Posted invoice totals - Posted receipt totals
```

- A positive amount is shown as **Receivable**.
- Zero is shown as **Settled**.
- A negative amount is shown as **Advance**.

### Supplier

```text
Supplier current balance = Opening balance + Posted purchase totals - Posted payment totals
```

- A positive amount is shown as **Payable**.
- Zero is shown as **Settled**.
- A negative amount is shown as **Advance**.

Cancelled invoices, receipts, purchases, and payments are excluded from current balance calculations automatically. No balance update is needed after posting or cancellation because the list calculates the latest value from transaction history.

## Statement Period

Use the Financial Year selector to load a configured Financial Year. The From and To fields can then narrow the statement to a custom date range inside or outside that year.

The system calculates:

```text
Period opening = Master opening balance
                 + Posted document totals before From date
                 - Posted settlement totals before From date

Closing balance = Period opening
                  + Posted documents in the period
                  - Posted settlements in the period
```

This means the statement remains correct even when you choose a mid-year or custom start date.

## Dashboard Summary

The statement dashboard shows:

- Customer/Supplier identity, contact, GSTIN, location, and active state
- Master opening balance entered during setup
- Period opening balance brought forward
- Total Invoices or Purchases in the selected period
- Total Receipts or Payments in the selected period
- Current Closing Receivable, Payable, or Advance
- Total posted Invoices/Purchases
- Paid, Partially Paid, and Unpaid document counts

The Paid/Partially Paid/Unpaid cards are based on allocation status of posted invoices or purchases. They are separate from account closing balance.

## Transaction Statement

The Statement tab shows:

| Column | Meaning |
| --- | --- |
| Date | Transaction date; B/F represents balance brought forward at the selected start date |
| Reference | Invoice, Receipt, Purchase, Payment, or B/F number |
| Transaction | Transaction type and description/reference |
| Debit | Debit side of the party account |
| Credit | Credit side of the party account |
| Running balance | Account balance after that row |

### Customer Ledger Direction

| Entry | Debit | Credit | Balance effect |
| --- | --- | --- | --- |
| Opening receivable | Yes | - | Increases receivable |
| Invoice | Yes | - | Increases receivable |
| Receipt | - | Yes | Reduces receivable |
| Customer advance | - | Yes | Produces negative/advance balance when receipts exceed dues |

### Supplier Ledger Direction

| Entry | Debit | Credit | Balance effect |
| --- | --- | --- | --- |
| Opening payable | - | Yes | Increases payable |
| Purchase | - | Yes | Increases payable |
| Payment | Yes | - | Reduces payable |
| Supplier advance | Yes | - | Produces negative/advance balance when payments exceed dues |

This difference is normal accounting presentation: customers are receivable accounts and suppliers are payable accounts.

## Invoice/Purchase History

The second tab lists all Invoices for a Customer or Purchases for a Supplier in the selected period, including:

- Document number and date
- Due date
- Linked Site, when present
- Total amount
- Amount received/paid against that specific document
- Remaining document balance
- Payment status
- Posted or Cancelled document status

Cancelled records remain visible in history for audit, but do not contribute to the financial summary or statement running balance.

## Receipt/Payment History

The third tab lists Receipts for a Customer or Payments for a Supplier in the selected period, including:

- Receipt/Payment number and date
- Linked Site, when present
- Payment method and external reference
- Total amount
- Allocated amount
- Unallocated amount/party advance
- Posted or Cancelled status

An unallocated Receipt does not mark an Invoice Paid because it has no invoice allocation. It still reduces the Customer's overall account balance because money has been received. The same principle applies to an unallocated Supplier Payment: it creates Supplier advance and reduces the overall payable.

## Print and CSV Export

Use the top-right Print icon to create a clean full-period statement containing party/company details, summary, and the complete ledger. Browser pop-ups must be allowed.

Use the CSV icon to download the complete filtered statement. It includes Date, Reference Number, Transaction Type, Description, Debit, Credit, and Running Balance. It is not limited to the currently visible statement-table page.

## Important Rules

- The balance is calculated from all posted transaction amounts, not only allocated amounts.
- Invoice/Purchase payment status still uses allocations and can remain Pending while an overall party advance exists.
- Opening balance is included as a brought-forward account balance. It is not an Invoice or Purchase allocation row.
- Cancellation reverses the posted transaction's contribution automatically.
- Editing a Customer/Supplier master does not allow manual modification of Current/Closing balance.
- Customer Receipt advance allocation is not currently available as a later UI workflow; allocate receipts correctly during entry when possible.
- Supplier Payment advances can be allocated later through the Supplier advance allocation workflow.

See [Invoices and Receipts](07-invoices-and-receipts.md), [Purchases and Payments](08-purchases-and-payments.md), and [End-to-End Workflows](15-end-to-end-workflows.md).
