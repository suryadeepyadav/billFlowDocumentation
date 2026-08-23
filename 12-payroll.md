# Payroll

## What Is This Module?

Payroll converts approved attendance and effective employee compensation into employee earnings, deductions, net payable salary, advance recovery, and salary payment history.

BillFlow supports:

- Daily-wage workers
- Monthly-salary employees
- Overtime by fixed hourly rate or multiplier
- Recurring and one-time earnings/deductions
- Employee advances and payroll recovery
- Partial or full salary payments
- Payroll summaries and employee payslips

Payroll is independent from Site Management. Payroll expense is not currently posted to Site Costing or Site Ledger.

## Why Is It Used?

Use Payroll to create a controlled monthly or custom-period salary process:

1. Attendance is entered and approved.
2. A payroll period is created.
3. BillFlow calculates employee entries.
4. Authorized users review and adjust entries.
5. Payroll is approved, locking included attendance.
6. Payroll is posted, creating salary balances and applying advance recoveries.
7. Salary payments are recorded and tracked.

## Module Tabs

- **Payroll runs**: Create, calculate, approve, post, cancel, and inspect payroll.
- **Advances**: Record and monitor money advanced to employees.
- **Salary payments**: Review posted and cancelled salary payments.
- **Reports**: Generate a payroll-run summary and print employee payslips.
- **Settings**: Configure attendance payable values and payroll calculations.

# Payroll Settings

## Why Settings Matter

Payroll settings affect attendance payable units, overtime rounding/rates, and monthly salary deduction calculations. Review them before entering production attendance or creating a run.

A payroll run keeps a settings snapshot, providing context for how that run was calculated.

## Settings Fields

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Standard daily minutes | Yes | Expected minutes in a normal day, such as 480 | Fallback for attendance/overtime when compensation or Shift does not provide a value |
| Monthly salary divisor | Yes | Fixed 26, Fixed 30, Calendar days, or Working days | Determines per-day unpaid deduction and monthly overtime hourly base |
| Weekly off days | Yes for Working days method | Select weekly rest day(s) | Excluded when calculating the Working days divisor |
| Default overtime method | Yes | Fixed hourly or Multiplier | Used when employee compensation says Inherit |
| Default overtime rate | Conditional | Positive hourly amount | Used by Fixed hourly method when compensation has no specific rate |
| Default overtime multiplier | Conditional | Positive factor, such as 1.5 | Multiplies calculated base hourly rate |
| Minimum overtime minutes | Yes | Minimum candidate, such as 30 | Smaller overtime candidates become zero |
| Overtime rounding minutes | Yes | 1, 15, 30, or 60 | Candidate overtime is rounded down to this interval |
| Half-day payable units | Yes | Value from 0 to 1, commonly 0.5 | Payable portion of a Half Day |
| Paid-leave payable units | Yes | Value from 0 to 1, commonly 1 | Payable portion of Paid Leave |
| Week-off payable units | Yes | Value from 0 to 1, commonly 1 | Payable portion of Week Off |
| Holiday payable units | Yes | Value from 0 to 1, commonly 1 | Payable portion of Holiday |

## Salary Divisor Methods

| Method | Divisor used |
| --- | --- |
| Fixed 26 days | 26 |
| Fixed 30 days | 30 |
| Calendar days | Inclusive number of calendar days in the payroll period |
| Working days | Inclusive period days excluding configured weekly-off weekdays |

The salary divisor is used for unpaid-day deductions and monthly employee hourly-rate calculations. Monthly proration for joining/leaving is separately based on eligible calendar days in the selected payroll period.

# Payroll Runs

## Important Terms

- **Payroll run**: One payroll calculation for a defined period.
- **Payroll entry**: One employee's calculation inside a run.
- **Base pay**: Daily-wage or monthly-salary amount before overtime and additional lines.
- **Gross amount**: Base pay + overtime + earnings.
- **Deductions**: Recurring deductions + manual deductions + advance recovery.
- **Net payable**: Gross - deductions, never below zero.
- **Outstanding**: Net payable not yet covered by posted salary payments.
- **Compensation snapshot**: Employee rate/setup copied into the payroll entry for historical accuracy.
- **Settings snapshot**: Payroll settings captured for the run.
- **Carried-forward deduction warning**: Requested deductions exceed gross; resolve before approval.

## Create Payroll Run Fields

| Field | Required | What to enter | Notes |
| --- | --- | --- | --- |
| Payroll label | No | Friendly label, such as August 2026 | Defaults from the period start month/year |
| Period start | Yes | First included date | Immutable after run creation |
| Period end | Yes | Last included date | Must be on/after start; maximum period is 62 days |
| Payroll number | Generated | Nothing | Assigned from Payroll sequence |

BillFlow prevents a non-cancelled payroll run from overlapping another active run's period.

## Payroll Run Statuses

| Status | Meaning | Main allowed actions |
| --- | --- | --- |
| Draft | Period exists but entries are not finalized | Calculate, Cancel |
| Calculated | Employee entries/totals generated | Recalculate, Adjust, Approve, Cancel |
| Approved | Entries accepted and attendance locked | Post, Cancel |
| Posted | Salary liability created and advance recovery applied | Record payments, print, Cancel subject to reversal rules |
| Cancelled | Reversed/inactive run | View/retain history |

## Calculate Payroll

Select **Calculate** on a Draft or Calculated run. BillFlow:

1. Finds employees whose joining/leaving dates overlap the period.
2. Finds the latest compensation effective for each employee in the period.
3. Includes only Approved or already Locked attendance.
4. Summarizes payable days, unpaid days, regular time, and approved overtime.
5. Calculates base pay and overtime pay.
6. Adds recurring allowances and recurring deductions.
7. Preserves existing manual lines when recalculating.
8. Proposes automatic advance recoveries from oldest open advances.
9. Produces totals and warnings.

Draft or Submitted attendance is excluded. BillFlow displays a warning count; it does not silently treat those records as approved.

An employee with missing compensation is skipped and listed in warnings. Resolve warnings before approval.

## Daily-Wage Calculation

```text
Base pay = Daily base rate x Payable attendance day units
```

Example:

```text
Daily rate: Rs. 800
Payable units: 24.5
Base pay: 800 x 24.5 = Rs. 19,600
```

Only approved attendance contributes payable units. A missing attendance day does not automatically become Present, Absent, Week Off, or Holiday.

## Monthly-Salary Calculation

BillFlow first prorates salary for the employee's joining/leaving overlap, then deducts unpaid units:

```text
Eligible days = Calendar days employee overlaps the payroll period
Prorated salary = Monthly base rate x (Eligible days / Period calendar days)
Unpaid deduction = (Monthly base rate / Salary divisor) x Unpaid day units
Base pay = Prorated salary - Unpaid deduction
```

Unpaid units include:

- Absent: 1
- Unpaid Leave: 1
- Unpaid remainder of Half Day: `1 - configured Half-day payable units`

Base pay is never reduced below zero.

Example with no joining/leaving proration:

```text
Monthly salary: Rs. 30,000
Divisor: 30
Unpaid units: 2
Unpaid deduction: 30,000 / 30 x 2 = Rs. 2,000
Base pay: Rs. 28,000
```

## Overtime Pay Calculation

Payroll uses Approved overtime minutes from Attendance. The employee must have Overtime eligible enabled.

### Fixed Hourly

```text
Overtime pay = Approved overtime hours x Fixed overtime hourly rate
```

The employee-specific rate is used first; otherwise the default payroll rate is used.

### Multiplier

For a daily-wage employee:

```text
Base hourly rate = Daily base rate / Standard daily hours
Overtime hourly rate = Base hourly rate x Multiplier
```

For a monthly-salary employee:

```text
Base hourly rate = Monthly base rate / (Salary divisor x Standard daily hours)
Overtime hourly rate = Base hourly rate x Multiplier
```

Then:

```text
Overtime pay = Approved overtime hours x Overtime hourly rate
```

If Compensation uses **Inherit**, BillFlow uses the default method/rate or multiplier from Payroll Settings.

## Earnings, Deductions, and Net Pay

```text
Gross = Base pay + Overtime pay + Recurring earnings + Manual earnings
Total deductions = Recurring deductions + Manual deductions + Advance recovery
Net payable = Gross - Total deductions
```

BillFlow does not approve a run while deductions exceed gross. Adjust or remove deductions instead of relying on a negative salary.

## Adjust One Payroll Entry

Adjustment is available only while the run is Draft or Calculated.

### Adjustment Fields

| Field | Required | What to enter |
| --- | --- | --- |
| Additional earnings - Name | Required per used line | Bonus/allowance description |
| Additional earnings - Amount | Required per used line | Positive one-time amount |
| Additional deductions - Name | Required per used line | Deduction description |
| Additional deductions - Amount | Required per used line | Positive one-time amount |
| Employee advance | Required per recovery line | Open/partially recovered advance for this employee |
| Recovery amount | Required per recovery line | Positive amount within advance and available salary balance |
| Payroll notes | No | Internal explanation for the adjustment |

Recurring lines come from Compensation and cannot be edited in this dialog. Change future recurring setup through employee compensation; use manual lines for this run only.

Recalculate after attendance or compensation changes. Existing manual adjustments are preserved by recalculation.

## Approve Payroll

Approval is available only for a Calculated run and requires Payroll **Approve** permission.

Before approval, BillFlow checks that:

- Employee entries exist.
- No deduction exceeds gross pay.
- Attendance within the period is resolved for payroll.
- The run is still in Calculated status.

Approval locks the Approved attendance records included by the run. Review warnings, employee totals, and adjustments before confirming.

## Post Payroll

Posting is available only for an Approved run. Posting:

- Creates employee salary balances/ledger accruals.
- Applies payroll advance recoveries to employee advances.
- Makes Salary Payment available.
- Changes the run to Posted.

Approval and Posting are intentionally separate: approval confirms calculations, while posting recognizes the payable amounts.

# Employee Advances

## What Is an Advance?

Money paid to an employee before salary, intended to be recovered from one or more future payroll runs.

## Advance Fields

| Field | Required | What to enter | Notes |
| --- | --- | --- | --- |
| Employee | Yes | Active employee | Owner of the advance |
| Advance date | Yes | Date paid | Used for ordering recoveries |
| Advance amount | Yes | Positive amount | Original outstanding advance |
| Recovery per payroll | No | Non-negative planned deduction | Limited to advance amount; zero means no automatic recovery |
| Payment method | No; defaults to Cash | Cash, Bank Transfer, UPI, Cheque, or Other | Reference only |
| Reference number | No | Bank/UPI/cheque reference | Traceability |
| Notes | No | Reason or terms | Internal context |
| Advance number | Generated | Nothing | Assigned from Employee Advance sequence |

## Advance Statuses

| Status | Meaning |
| --- | --- |
| Open | Nothing or not all has been recovered |
| Partially Recovered | Some amount recovered; balance remains |
| Settled | Entire amount recovered |
| Cancelled | Advance cancelled before recovery |

Automatic recovery uses open advances from oldest to newest and never exceeds the employee's available net pay. Recovery is applied permanently only when Payroll is Posted.

An advance can be cancelled only before any recovery has been posted. Cancellation requires a reason.

# Salary Payments

## When Can Salary Be Paid?

Salary Payment is available only after Payroll is Posted and an employee entry has an outstanding amount.

## Salary Payment Fields

| Field | Required | What to enter | Notes |
| --- | --- | --- | --- |
| Employee/payroll | Read-only | Nothing | Taken from selected payroll entry |
| Payment date | Yes | Date salary was paid | Payment history date |
| Amount | Yes | Positive amount up to outstanding | Supports partial payments |
| Payment method | No; prefilled | Cash, Bank Transfer, UPI, Cheque, or Other | Employee preference is used when available |
| Reference number | No | Bank/UPI/cheque reference | Recommended for non-cash payments |
| Notes | No | Internal payment note | Optional |
| Payment number | Generated | Nothing | Assigned from Salary Payment sequence |

## Employee Payment Status

| Status | Meaning |
| --- | --- |
| Unpaid | No posted salary payment |
| Partially Paid | Some net salary paid, outstanding remains |
| Paid | Posted payments equal net payable |

A salary payment can be cancelled with permission. Cancellation restores the employee entry's outstanding amount and keeps an audited payment record with Cancelled status.

# Reports and Payslips

## Payroll Report

1. Open **Payroll > Reports**.
2. Select a payroll run.
3. Generate the report.

The report includes employee count, gross, deductions, net payable, outstanding, and employee-level Base, Overtime, Gross, Deductions, and Net amounts.

## Payslip

Open a payroll run and use **Print payslip** on an employee entry. A payslip uses the captured employee/compensation data and the run calculation. Permit browser pop-ups for printing.

Review payslips before distribution, especially manual adjustments, advance recovery, payment status, and company information.

# Cancelling and Correcting Payroll

## Correct a Draft or Calculated Run

1. Correct attendance/compensation if needed.
2. Recalculate the run.
3. Edit one-time adjustments.
4. Recalculate or review totals again.

## Cancel an Approved or Posted Run

Cancellation requires Payroll **Cancel** permission and a reason.

For a Posted run:

1. Cancel every posted salary payment for the run.
2. Cancel the payroll run.
3. BillFlow reverses posted advance recoveries.
4. BillFlow reverses salary accrual balances.
5. Included Locked attendance returns to Approved.

You can then Reopen attendance, correct it, and create/recalculate payroll again. Cancelled payroll remains in history; it is not deleted.

# Permissions

| Task | Required Payroll permission |
| --- | --- |
| Open lists/reports/settings | List |
| View payroll details | View |
| Create run, advance, or salary payment | Insert |
| Calculate/recalculate and adjust entries/settings | Update |
| Cancel advances or salary payments | Cancel |
| Approve and post payroll | Approve |
| Cancel payroll run | Cancel |
| Print summary/payslip | Print |
| Export lists | Export |

Menu access also depends on the Employees, Attendance, and Payroll subscription features being enabled.

# Recommended Monthly Workflow

1. Verify Payroll Settings before the period begins.
2. Complete daily attendance.
3. Review the Attendance Monthly Report.
4. Submit and approve all attendance in the payroll period.
5. Confirm each employee has correct effective Compensation.
6. Record any employee advances.
7. Create a non-overlapping Payroll Run.
8. Calculate and review warnings.
9. Review each employee's attendance, base pay, overtime, recurring lines, and advance recovery.
10. Add one-time earnings/deductions where required.
11. Recalculate/review totals.
12. Approve the run to lock attendance.
13. Post the run to create salary balances.
14. Record salary payments.
15. Print reports and payslips.

# Common Mistakes

- Creating payroll before attendance is Approved.
- Assuming missing days are automatically counted as Absent or Week Off.
- Selecting the wrong monthly salary divisor.
- Confusing calculated overtime with approved overtime.
- Leaving employee Overtime eligible off and expecting overtime pay.
- Using a future or incorrect compensation effective date.
- Forgetting that compensation and settings are snapshotted in payroll.
- Posting before reviewing manual adjustments and warnings.
- Recording an advance recovery larger than available salary.
- Expecting salary payments before the run is Posted.
- Cancelling payroll before cancelling its salary payments.
- Expecting payroll to update Site Costing.

Continue with [Users, Permissions, and Subscription](13-users-permissions-and-subscription.md).
