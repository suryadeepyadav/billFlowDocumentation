# Users, Permissions, and Subscription

## What Is This Area?

BillFlow uses three separate controls for access:

1. **Tenant subscription**: What product features the company has purchased from SYV Cloud.
2. **User permissions**: What an individual user may do inside those enabled features.
3. **Record state/business rules**: What actions are valid for the current document status.

All three must allow an action. For example, a user with Invoice Approve permission still cannot access Invoices when the tenant's `invoices` feature is disabled, and a permitted user still cannot cancel an invoice that has active receipts.

# User Management

## Why Is It Used?

Create a separate account for each person who uses BillFlow. Separate accounts provide:

- Individual authentication
- Least-privilege access
- Clear audit history
- Immediate deactivation when someone leaves
- Role-appropriate menus and actions

Do not share the first-admin password among the team.

## User Fields

| Field | Required | What to enter | Notes |
| --- | --- | --- | --- |
| Full name | Yes | User's real/working name | Appears in user and audit information |
| Username | Yes | Unique login name using allowed letters, numbers, `_`, `@`, `.`, or `-` | Tenant ID is not entered on the login page |
| Role | Yes | A built-in role | Applies a permission starting point |
| Password | Yes when creating | At least 8 characters | Stored securely as a hash |
| New password | No when editing | Enter only when changing password | Leaving blank keeps existing password |
| Email | No | Valid email address | Contact/reference |
| Phone | No | Valid phone number | Contact/reference |
| Address | No | User address | Optional profile detail |
| Active | No; defaults on | Turn off to block login | Prefer the dedicated Deactivate action for clarity |

Creating users is subject to the tenant's subscription user limit.

## Add a User

1. Open **Administration > Users & Permissions**.
2. Select Add User.
3. Enter identity and login fields.
4. Choose the closest Role.
5. Save.
6. Open the row's Permissions action.
7. Review and customize the permission matrix.
8. Test the account's normal workflow.

Creating a user assigns the selected role's default permissions. Role defaults should always be reviewed for the person's actual responsibilities.

## Edit or Reset a Password

Open Edit User. Change profile fields as needed. To reset the password, enter a New password; leave it blank to preserve the current password.

Changing a password invalidates older credentials/tokens according to the authentication policy. Ask the user to sign in again.

## Deactivate and Reactivate

### Deactivate

- Requires confirmation.
- Blocks new access immediately.
- Signs out active sessions.
- Preserves documents and audit history created by the user.

The currently signed-in user cannot deactivate their own account from the row action. The First Admin cannot be deactivated.

### Reactivate

Reactivate restores account access with the saved role and permissions. Review the permissions and reset the password when appropriate.

# First Admin

The first account created with the tenant is a protected recovery administrator.

- It cannot be deactivated.
- It must keep the Admin role.
- Permission middleware prevents it from being locked out.
- It should be protected with a strong unique password.

Use additional named Admin accounts for normal administration and keep the First Admin available for recovery.

# Roles

## What Is a Role?

A role is a predefined permission template. Selecting a role in the Permissions dialog replaces the on-screen matrix with that role's defaults; the changes become effective only after Save.

The saved per-user matrix is authoritative. Two users with the same role can have different permissions after customization.

## Built-In Roles

| Role | Intended starting point |
| --- | --- |
| Admin | Full product administration and all actions |
| Manager | Broad operating access, including workforce/payroll; limited administration |
| Employee | Basic sales/customer/site operating access without administration or workforce access |
| Accountant | Accounting, payroll, invoices, receipts, purchases, payments, expenses, and financial reports |
| Site Manager | Site operations, site work, expenses, and attendance supervision; no payroll |
| Sales User | Customers, quotations, sales invoice creation/printing, and read-only supporting information |
| Store Keeper | Inventory and purchase entry with supporting supplier/site visibility |
| HR Manager | Employees, attendance, payroll, related reports, and read-only administration context |
| Attendance Supervisor | Employee list plus attendance entry, update, approval, and dashboard |

These descriptions summarize defaults, not immutable rules. Customize the matrix to match company policy.

# Permission Matrix

## Permission Actions

| Permission | What it generally allows |
| --- | --- |
| List | Load/list records and list endpoints |
| Insert | Create new records or transactions |
| View | Open the module/page and view record details; module navigation generally requires View |
| Update | Edit records, save changes, or perform update-style workflows |
| Delete | Deactivate master/user records where the UI uses lifecycle deactivation |
| Print | Print documents, reports, or table output |
| Export | Export table/report data |
| Approve | Approve controlled workflows such as attendance or payroll |
| Cancel | Cancel/reverse posted or controlled transactions |

Permission names are generic. Their exact effect depends on the module and record status. BillFlow normally uses cancellation/deactivation rather than permanent deletion.

## Permission Modules

| Module | Controls |
| --- | --- |
| Dashboard | Dashboard access and summary data |
| Employees | Employees, compensation, Work Locations, and Shifts |
| Attendance | Daily entry, register, reports, submission, approval, reopen |
| Payroll | Runs, settings, advances, salary payments, reports, posting/reversal |
| Customers | Customer master |
| Suppliers | Supplier master |
| Inventory | Items, Categories, Units, stock, adjustments, movements |
| Quotations | Quotation lifecycle and conversion actions |
| Invoices | Sales invoice creation/view/cancellation |
| Receipts | Customer receipts and allocations |
| Purchases | Purchase creation/view/cancellation |
| Payments | Supplier payments, allocations, and Payment Methods navigation |
| Sites | Site master, site materials, attachments, and site overview actions |
| Site Expenses | Expense Heads and site expense transactions |
| Site Ledger | Fund transfers and site ledger/cash visibility |
| Site Work History | Site work-history entry, update, status, cancellation |
| Reports | Business reports and full report exports |
| Users | User account lifecycle |
| Permissions | Permission matrix and Users & Permissions menu access |
| Settings | Company, tax, financial year, sequence, audit, appearance, subscription tabs |

Some pages involve more than one module. For example, Payroll requires its own permissions and licensed Employees/Attendance dependencies; site operations use separate Site, Expense, Ledger, and Work History permissions.

## Configure Permissions

1. Open the user's row Actions menu.
2. Select **Permissions**.
3. Choose a Role if a different default template is needed.
4. Check only required module/action combinations.
5. Save.
6. Ask the user to refresh or sign in again.
7. Test the exact API workflow, not only whether the menu appears.

### Practical Permission Design

- Give View and List where a user must browse records.
- Add Insert only for modules where they create data.
- Add Update only where they correct/manage data.
- Restrict Approve and Cancel to accountable supervisors.
- Restrict Settings, Users, Permissions, and Payroll to trusted staff.
- Give Print/Export according to data-handling policy.
- Review permissions whenever a person's job changes.

# Subscription and License

## What Is the Subscription?

The tenant subscription is controlled by the centralized SYV Cloud product/license system. BillFlow receives and stores a synchronized entitlement containing:

- Product code
- Package name and type
- Enabled package features
- Package limits
- Active/inactive state
- Expiry date
- Last synchronization time

The secret/license key is not displayed to ordinary users.

## Where to View It

Open **Administration > Settings > Subscription**. This tab is read-only in BillFlow. Package changes should be made in SYV Cloud and then synchronized.

## Feature Keys

The BillFlow package may use these feature keys:

| Feature key | Product area enabled |
| --- | --- |
| customers | Customer master |
| quotations | Quotations |
| invoices | Sales invoices |
| receipts | Customer receipts |
| suppliers | Supplier master |
| purchases | Purchases |
| payments | Supplier payments and Payment Methods |
| inventory | Stock Control, Items, Categories, Units |
| sites | Site master and core site area |
| siteExpenses | Expense Heads and Site Expenses |
| siteWorkHistory | Site Work History |
| employees | Employees, Work Locations, Shifts |
| attendance | Attendance, together with employees |
| payroll | Payroll, together with employees and attendance |
| reports | Reports |
| users | Users & Permissions feature entitlement |
| settings | Settings |

Site Ledger is governed through the Sites package context and its own user permission; package design should keep site-related dependencies together.

## Feature Dependencies

- Attendance navigation requires both `employees` and `attendance`.
- Payroll navigation requires `employees`, `attendance`, and `payroll`.
- Items, Categories, Units, and Stock Control all use `inventory`.
- Payment Methods uses `payments`.

When packaging a dependent module, include its prerequisite features.

## Package Limits

Package limits can include values such as:

- Users
- Customers
- Invoices per month
- Sites

BillFlow enforces the user limit during user creation. Other limits are synchronized entitlement metadata and may be enforced by the relevant product workflow as the application evolves. A `LICENSE_LIMIT_REACHED` response means the tenant must reduce usage or upgrade/synchronize the package.

## License States

| Condition | Effect |
| --- | --- |
| Active and not expired | Licensed features can be used subject to permissions |
| Feature disabled | Menu/action hidden and backend rejects feature access |
| Subscription inactive | Protected application access is blocked |
| Subscription expired | User is directed to the license-expired experience |
| Sync unavailable | Existing entitlement behavior depends on server configuration; an administrator should verify cloud integration |

Never enable a frontend menu without the matching backend entitlement. BillFlow checks features on the server as well as in navigation.

## Renew an Expired or Inactive Subscription

After a correct BillFlow username and password are verified for an expired or inactive mapped subscription:

1. BillFlow opens the License Expired page without creating a normal application session.
2. Select **Manage subscription**.
3. BillFlow securely opens the matching SYV Client subscription page without asking for another portal login.
4. Complete the renewal or activation in SYV Client.
5. SYV Client returns to BillFlow's license return page.
6. BillFlow checks its own latest synchronized subscription status.
7. If synchronization is still pending, wait briefly and select **Check again**.
8. When active, sign in to BillFlow again if the original expired login did not have a normal session.

The renewal identity lasts about five minutes and is stored only for the current browser tab. It cannot open normal BillFlow APIs. No username, password, Tenant ID, license key, renewal token, or portal secret is placed in the browser URL.

For a Missing License or Product Mismatch, use the normal portal/support option and ask an administrator to correct the tenant/product mapping. Those conditions are not treated as ordinary renewals.

# Access Troubleshooting

## Menu Is Missing

Check in this order:

1. Is the required package feature enabled?
2. Are dependency features enabled?
3. Does the user have View permission for the module?
4. Is the subscription active and unexpired?
5. Has the user refreshed/signed in after changes?

## Page Opens but an Action Says No Permission

The user may have View but not Insert, Update, Approve, Cancel, Print, or Export. Open the permission matrix and check the action required by that endpoint.

## All APIs Return 403

Possible causes include:

- Feature not licensed
- Permission record missing or action bit not granted
- Subscription inactive/expired
- Account deactivated
- Old login token after password/access changes

Sign out/in after correcting access. The First Admin can be used to recover tenant permissions.

## Recommended Security Routine

- Use named accounts; never shared usernames.
- Use strong unique passwords.
- Keep First Admin credentials protected.
- Review active users and permission matrices regularly.
- Deactivate users immediately when access is no longer required.
- Restrict Approve, Cancel, Settings, Users, Permissions, and exports.
- Review the Audit tab after sensitive changes.
- Manage package entitlements only through authorized SYV Cloud administration.

Continue with [Dashboard, Reports, Printing, and Exports](14-dashboard-reports-printing-and-exports.md).
