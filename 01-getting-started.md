# Getting Started

## What Is BillFlow?

SYV BillFlow is a tenant-based business application for sales, purchasing, inventory, site operations, workforce attendance, and payroll. It keeps master data, financial documents, stock movements, site cash, employee attendance, and payroll history in one workspace.

## Who Should Read This Guide?

- A new company administrator setting up BillFlow
- A new team member signing in for the first time
- A manager deciding the correct order for configuring modules
- A user who cannot see a menu or action

## Signing In

The login form contains only two fields.

| Field | Required | What to enter |
| --- | --- | --- |
| Username | Yes | The username created by the company administrator or during tenant registration |
| Password | Yes | The password assigned to the account; it is case-sensitive |

There is no Tenant ID field on the login page. BillFlow resolves the user's tenant and includes it in the authenticated session. Never put a Tenant ID into the Username field unless it is genuinely part of the assigned username.

Use the eye icon in the password field to temporarily show or hide the entered password.

## Understanding the Workspace

A **tenant** is one subscribed company workspace. Data is isolated by tenant, so customers, invoices, sites, employees, and settings from one company are not mixed with another company.

After login:

- The bottom of the sidebar shows the current company name and Tenant ID.
- The sidebar groups available modules under Sales, Purchasing, Inventory, Sites & Expenses, Workforce, and Administration.
- Missing modules usually indicate a subscription feature or user permission restriction.
- The current primary color is a company-wide preference.
- Light or dark mode is a browser/user preference and is not currently synchronized as a tenant-wide setting.

## First-Time Setup Checklist

Use this order for a new workspace. It prevents missing dropdown choices and incorrect tax or numbering behavior.

1. Open **Settings > Company** and verify business identity, address, state, state code, GSTIN, PAN, and logo.
2. Open **Settings > Tax** and configure GST behavior before creating quotations, invoices, or purchases.
3. Open **Settings > Financial years** and confirm the correct active year.
4. Open **Settings > Sequences** and review document prefixes, financial-year codes, counters, and padding.
5. Create common **Units** and **Categories**.
6. Create **Items & Services**, including stock opening balances and minimum stock where needed.
7. Create **Payment Methods** and mark the most common one as default.
8. Create **Expense Heads** if Site Expenses will be used.
9. Add **Customers** and **Suppliers**, paying special attention to their state codes.
10. Add users and assign roles and permissions.
11. If Workforce is enabled, create work locations, shifts, employees, compensation, and payroll settings.
12. Enter opening stock and opening customer/supplier balances only after checking the values from the previous system.

See [Company, Tax, Financial Year, and Other Settings](03-company-tax-and-financial-settings.md) for exact fields.

## Minimum Setup by Workflow

### To Create a Quotation

You need:

- An active customer
- At least one line with an item/service name, quantity, and rate
- Correct company tax settings

An item master is convenient but not mandatory for a quotation line. A free-text line is treated as a service and does not affect stock.

### To Create an Invoice

You need:

- An active customer
- At least one valid line
- Sufficient warehouse stock for every selected stock item

The invoice can be created directly or from an accepted quotation.

### To Record a Receipt

You need:

- An active customer
- A positive received amount

A payment method and invoice allocation are optional. Any amount not allocated to an invoice remains recorded as unallocated customer advance.

### To Create a Purchase

You need:

- An active supplier
- At least one valid line

Selecting a site receives stock items directly at that site. Leaving the site empty receives them into the warehouse.

### To Record Attendance and Payroll

You need:

- Active employees with current compensation
- Payroll settings
- Optional work locations and shifts
- Complete check-in/check-out sessions for Present and Half Day attendance before submission
- Approved attendance before payroll calculation

## Required Versus Important Optional Fields

BillFlow validates required fields when you save. Some optional fields have major downstream effects:

| Field | Why it matters even when optional |
| --- | --- |
| Customer/supplier state code | Determines intra-state CGST/SGST versus inter-state IGST |
| HSN/SAC | Helps produce tax-compliant item descriptions |
| Due date | Drives overdue balances and aging reports |
| Payment method and reference | Makes bank, UPI, cheque, and cash reconciliation easier |
| Site link | Attributes purchases, receipts, payments, and financial activity to the site |
| Work location and shift | Improves attendance context and automatic time defaults |
| Notes and terms | Preserve commercial or operational context on records and prints |

## Quick Add from Dropdowns

Relevant dropdowns include an Add New button. You can create the missing master without abandoning the current workflow:

- Quotation or invoice: add a customer or item
- Receipt: add a customer or payment method
- Purchase: add a supplier or item
- Payment: add a supplier or payment method
- Item: add a category or unit
- Site: add a customer, expense head, payment method, or stock item

After the new record is saved, BillFlow refreshes the dropdown and selects it where appropriate.

The Add New option is hidden when the subscription does not include the related feature or the user lacks Insert permission.

## Safe Working Habits

- Verify the active financial year before the first transaction of a new year.
- Enter state codes before creating GST documents.
- Use draft quotation and attendance states for work still under review.
- Review allocations before posting receipts and supplier payments.
- Confirm available warehouse or site stock before issuing material.
- Do not approve attendance until overtime has been reviewed.
- Do not post payroll until earnings, deductions, and advance recoveries are final.
- Use cancellation actions to reverse posted records; do not expect permanent deletion.
- Enter a meaningful cancellation or reopening reason for audit clarity.

## When a Page Says No Access

Check these in order:

1. Is the module included in the tenant's SYV Cloud package?
2. Is the subscription active and not expired?
3. Does the user have at least List or View permission for the module?
4. Does the intended action require an additional permission such as Insert, Update, Approve, Cancel, Print, or Export?
5. Was the user's permission changed while they were signed in? Sign out and sign in again if needed.

Administrators can review [Users, Permissions, and Subscription](13-users-permissions-and-subscription.md). General errors are covered in [Troubleshooting and FAQ](18-troubleshooting-and-faq.md).

## Next Steps

- Learn the shared controls in [Navigation, Tables, and Common Actions](02-navigation-tables-and-common-actions.md).
- Configure the workspace with [Company, Tax, Financial Year, and Other Settings](03-company-tax-and-financial-settings.md).
- Follow a practical process in [End-to-End Workflows](15-end-to-end-workflows.md).
