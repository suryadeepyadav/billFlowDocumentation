# Employees and Compensation

## What Is the Workforce Master Module?

**Employees & Workers** maintains people, work locations, shifts, and compensation history used by Attendance and Payroll.

This workforce area is currently independent from Site Management:

- A Work Location is not a BillFlow Site.
- Attendance at a Work Location does not create Site Work History.
- Employee payroll is not included in Site Costing.
- These areas may be integrated in a future version, but users should not assume a link today.

## Module Tabs

- Employees
- Work locations
- Shifts

# Employees and Workers

## Why Is It Used?

Employee records provide:

- Identity and contact information
- Department and designation/trade
- Default attendance location and shift
- Daily wage or monthly salary setup
- Overtime method/rate
- Recurring allowances and deductions
- Payment preference and bank reference
- Compensation history used by payroll snapshots

## Important Terms

- **Employee code**: Generated unique workforce identifier.
- **Daily wage**: Base pay calculated from payable attendance day units.
- **Monthly salary**: Fixed monthly rate, prorated/deducted according to payroll settings and attendance.
- **Compensation**: Effective-dated wage/salary, overtime, allowance, and deduction setup.
- **Current compensation**: Latest active compensation record used for payroll.
- **Superseded compensation**: Older rate retained in history after a later effective rate is added.
- **Default shift/location**: Preselected attendance values; both remain optional.

## Employee Fields

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Employee code | Generated | Nothing | Assigned from employee sequence |
| Full name | Yes | Legal/working name | Main attendance/payroll identity |
| Phone | No | 10 to 15 digit phone when entered | Contact detail |
| Alternate phone | No | Secondary phone | Contact detail |
| Email | No | Valid email | Stored in lowercase |
| Designation / trade | No | Role/trade, such as Fabricator or Accountant | Shown in lists and reports |
| Department | No | Organizational group, such as Workshop or HR | Enables attendance/report filtering |
| Joining date | Yes | Employment start date | Controls payroll period eligibility/proration |
| Date of birth | No | Employee birth date | Reference only |
| Default work location | No | Active independent Work Location | Pre-fills daily attendance |
| Default shift | No | Active Shift | Pre-fills times/break and standard minutes |
| Address | No | Residential/contact address | Employee record |
| Payment preference | No; defaults to CASH | CASH, BANK_TRANSFER, UPI, CHEQUE, or OTHER | Pre-fills salary payment method |
| Bank name | No | Employee bank | Payment reference |
| Account number | No | Employee account | Payment reference |
| IFSC code | No | Bank IFSC | Input is normalized to uppercase |
| Emergency contact | No | Contact person's name | Safety/contact reference |
| Emergency phone | No | Valid contact phone | Safety/contact reference |
| Notes | No | Internal employee notes | Workforce context |

The employee's status/active state is managed through Deactivate and Reactivate actions rather than a visible switch in this form.

## Add an Employee

1. Open **Workforce > Employees & Workers > Employees**.
2. Select the plus icon in the table toolbar.
3. Enter employee fields.
4. Configure Initial compensation.
5. Save.

An employee cannot be created without an initial valid compensation record.

# Compensation

## Initial/Change Compensation Fields

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Effective from | Yes | Date this rate begins | Cannot be in the future in the current workflow |
| Payment structure | Yes | DAILY_WAGE or MONTHLY_SALARY | Selects base-pay method |
| Daily wage / Monthly salary | Yes | Positive base rate | Main pay amount |
| Standard daily minutes | No; normally defaults to 480 | Positive minutes, maximum 1440 | Employee-specific workday for overtime rate/candidate calculations; payroll default is fallback |
| Overtime method | No; defaults to INHERIT | INHERIT, FIXED_HOURLY, or MULTIPLIER | Chooses overtime pay rate method |
| Overtime hourly rate | Conditional | Zero or positive rate when FIXED_HOURLY | Amount paid per approved overtime hour |
| Overtime multiplier | Conditional | Zero or positive multiplier when MULTIPLIER/INHERIT display applies | Multiplies calculated base hourly rate |
| Eligible for overtime | No; defaults on | On or off | Off forces overtime pay rate to zero |
| Recurring allowance name | Conditional per added row | Meaningful name | Added to every payroll calculation using this compensation |
| Recurring allowance amount | Conditional per added row | Positive amount | Added to gross earnings |
| Recurring deduction name | Conditional per added row | Meaningful name | Added to every payroll deduction |
| Recurring deduction amount | Conditional per added row | Positive amount | Reduces net pay |
| Compensation notes | No | Reason/rate context | Preserved with compensation history |

Blank or zero recurring rows are ignored. Use the plus/minus controls to add or remove rows.

## Payment Structures

### Daily Wage

Base pay is:

`Daily wage x Payable attendance day units`

Examples of payable units are configured in Payroll Settings. By default, Present is 1, Half Day is 0.5, Paid Leave is 1, Unpaid Leave is 0, Week Off is 1, and Holiday is 1.

### Monthly Salary

Payroll begins with the monthly salary, prorates for the employee's eligible employment days in the payroll period, and deducts unpaid attendance using the configured salary divisor.

See [Payroll](12-payroll.md) for the exact formula.

## Overtime Methods

### Use Payroll Settings (INHERIT)

Uses the default method and rate/multiplier from Payroll Settings.

### Fixed Hourly Rate

Overtime pay is:

`Approved overtime hours x Employee overtime hourly rate`

If an inherited fixed rate is used, the Payroll Settings default fixed rate applies.

### Hourly Multiplier

BillFlow calculates a base hourly rate from Daily wage or Monthly salary and multiplies it by the employee/default overtime multiplier.

Only **approved overtime minutes** are paid.

## Change Compensation

Use the **Change compensation** row action on an active employee.

- Effective date cannot be in the future.
- It cannot be before the current compensation's effective date.
- Saving with the same effective date corrects the current compensation.
- Saving with a later effective date marks the old record SUPERSEDED and sets its Effective to date to the day before the new rate.
- Historical compensation remains visible in Employee details.

Payroll stores a compensation snapshot in each entry, so a later rate change does not rewrite an already calculated/posted payroll entry unless that run is still eligible for recalculation.

## Employee Details

The View action shows identity/default assignment details and compensation history:

- Effective from
- Wage type
- Base rate
- Overtime eligibility/method
- ACTIVE or SUPERSEDED status

## Deactivate and Reactivate Employee

### Deactivate

Deactivation:

- Requires confirmation.
- Sets the employee inactive.
- Sets Leaving date to the current date when one is not already present.
- Removes the employee from new daily attendance entry.
- Preserves attendance, payroll, advance, and payment history.

### Reactivate

Reactivation:

- Sets the employee active.
- Clears Leaving date.
- Makes the employee available for attendance again.

Review compensation before recording new attendance for a reactivated employee.

# Work Locations

## What Is a Work Location?

A reusable attendance location such as Head Office, Workshop, Warehouse, Client Location, or another named area. It is independent from Site Management.

### Work Location Fields

| Field | Required | What to enter |
| --- | --- | --- |
| Location code | Generated | Nothing; assigned from work-location sequence |
| Name | Yes | Unique location name |
| Location type | No; defaults to OTHER | OFFICE, WORKSHOP, WAREHOUSE, CLIENT_LOCATION, or OTHER |
| Address | No | Location address |
| Notes | No | Operational details |

Deactivate a location to hide it from new attendance sessions. Existing attendance keeps the reference. Reactivate to use it again.

# Shifts

## What Is a Shift?

A reusable work schedule that can prefill check-in, check-out, break, and standard daily minutes in Attendance.

### Shift Fields

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Shift code | Generated | Nothing | Assigned from shift sequence |
| Name | Yes | Unique shift name | Dropdown label |
| Start time | Yes | Scheduled check-in | Prefills attendance |
| End time | Yes | Scheduled check-out | Prefills attendance |
| Standard minutes | Yes | Positive expected worked minutes | Overtime begins above this value |
| Default break minutes | No; defaults to 60 in the form | Zero or positive break | Prefills attendance break |
| Grace minutes | No; defaults to 10 in the form | Zero or positive grace reference | Stored for schedule policy |
| Half-day threshold | Yes | Positive minutes | Stored for half-day policy |
| Night shift | No; switch | Turn on when check-out may occur the next day | Identifies overnight schedule |

Current daily attendance does not automatically mark Late or Half Day from Grace minutes or Half-day threshold. The user selects Attendance status; worked and overtime minutes are calculated from entered times.

Deactivate a shift to hide it from new attendance records. Existing records retain the shift.

## Permissions

The Employees permission module controls employees, compensation, work locations, and shifts in the current UI.

| Action | Permission |
| --- | --- |
| List | List |
| View employee/history | View |
| Add employee/location/shift | Insert |
| Edit/change compensation/reactivate | Update |
| Deactivate | Delete |
| Print/Excel | Print/Export |

## Recommended Workforce Setup Order

1. Review Payroll Settings.
2. Create Work Locations.
3. Create Shifts.
4. Add Employees with initial compensation.
5. Verify overtime eligibility and method.
6. Add recurring allowances/deductions.
7. Test one day's attendance and one test payroll before production use.

## Common Mistakes

- Creating an Employee without a correct initial rate.
- Using a future compensation date, which is not currently supported.
- Confusing Work Location with Site.
- Assuming Grace minutes automatically marks attendance late.
- Leaving Standard minutes incorrect and getting wrong overtime.
- Adding an allowance as a deduction or vice versa.
- Changing compensation after payroll without understanding snapshots.
- Deactivating an employee before completing required attendance/payroll for their final period.

Continue with [Attendance](11-attendance.md) and [Payroll](12-payroll.md).
