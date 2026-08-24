# Attendance

## What Is This Module?

Attendance records each employee's daily work status, working time, break, calculated overtime, and approval state. Approved attendance becomes an input to Payroll.

Attendance is currently part of the independent Workforce area. Selecting a Work Location does not update a BillFlow Site, Site Work History, Site Ledger, or Site Costing.

## Why Is It Used?

Use Attendance to:

- Mark employees Present, Absent, on Leave, on Week Off, or on Holiday.
- Record check-in and check-out times.
- Calculate regular working time and overtime candidates.
- Review and approve overtime before payroll.
- Maintain an auditable Draft, Submitted, Approved, and Locked workflow.
- Review a daily register and monthly attendance summary.

## Before Recording Attendance

1. Add employees and their current compensation.
2. Optionally create Work Locations and Shifts.
3. Set default Work Location and Shift on employees where useful.
4. Review Attendance and Payroll calculation settings.
5. Confirm the user has Attendance permissions.

See [Employees and Compensation](10-employees-and-compensation.md) and [Payroll](12-payroll.md).

## Module Tabs

- **Daily entry**: Enter or update attendance for one date.
- **Attendance register**: Search and manage saved attendance records.
- **Monthly report**: Review employee-wise attendance totals for a month.

# Daily Entry

## Daily Toolbar

| Control | Required | Purpose |
| --- | --- | --- |
| Work date | Yes | Date for which attendance is being recorded |
| Department | No | Limits the employee list to one department |
| Show all columns | No | Shows or hides Shift, Work Location, and Break columns |
| Reload | No | Reloads employees and saved attendance for the selected date |
| Mark all present | No | Marks editable rows Present and prefills available defaults |
| Save | No | Saves changed rows as Draft |
| Save menu | No | Offers Save & submit and, for approvers, Save & approve all |

The compact view hides Shift, Work Location, and Break to preserve space. Hiding these columns does not erase their saved values.

### Unsaved Changes Protection

When rows have unsaved changes, BillFlow warns before changing the date, department, reloading, leaving the page, or closing the browser tab. Save or intentionally discard the changes before continuing.

## Daily Summary

The summary band helps the operator check the current date before saving:

- Employees loaded
- Present count
- Absent/leave count
- Pending approval count
- Approved overtime

These are operational indicators for the selected daily sheet, not payroll totals.

## Daily Entry Fields

| Field | Required | What to enter | Notes |
| --- | --- | --- | --- |
| Employee | Read-only | Nothing | Shows employee code, name, department, or designation |
| Status | Yes | Present, Absent, Half Day, Paid Leave, Unpaid Leave, Week Off, or Holiday | Determines payable units and whether times are applicable |
| Shift | No | An active Shift | Prefills scheduled times, break, and standard minutes |
| Work location | No | An active independent Work Location | Attendance reference only; it is not a Site |
| Check-in | Conditional | Start time | Required before Submit/Approve for Present and Half Day |
| Check-out | Conditional | End time | Required before Submit/Approve for Present and Half Day |
| Break | No | Minutes not worked | Must be non-negative, no more than 720, and shorter than the work session |
| Worked / OT | Calculated | Nothing | Shows regular worked time and calculated overtime candidate |
| Workflow | Read-only | Nothing | Draft, Submitted, Approved, or Locked |
| Actions | Permission-based | View, Submit, Approve, or Reopen | Available actions depend on workflow and permissions |

Shift, Work Location, and Break are optional. For reliable overtime, however, use a Shift or ensure the configured standard daily minutes accurately represents the employee's schedule.

## Attendance Statuses

| Status | Meaning | Times used? | Default payable units |
| --- | --- | --- | --- |
| Present | Employee worked a full payable day | Yes | 1 |
| Absent | Employee did not work and is unpaid | No | 0 |
| Half Day | Employee worked a partial day | Yes | 0.5 |
| Paid Leave | Approved paid absence | No | 1 |
| Unpaid Leave | Approved unpaid absence | No | 0 |
| Week Off | Scheduled weekly rest day | No | 1 |
| Holiday | Paid organization/public holiday | No | 1 |

The Half Day, Paid Leave, Week Off, and Holiday payable values are configurable in Payroll Settings. The values above are defaults.

Changing a row to a non-working status clears its check-in, check-out, Work Location, and Break because those values no longer apply.

## Worked Time Calculation

For Present and Half Day rows:

```text
Elapsed minutes = Check-out - Check-in
Worked minutes = Elapsed minutes - Break minutes
Regular minutes = Lower of Worked minutes and Standard minutes
Overtime candidate = Worked minutes - Standard minutes
```

Standard minutes come from the selected Shift when available; otherwise the global standard daily minutes are used.

When check-out is earlier than or equal to check-in, BillFlow treats check-out as occurring on the following day. This supports overnight shifts. Always verify accidental reversed times before approval.

## Overtime Calculation

The Daily Entry page shows an overtime candidate. It is not payable overtime until approved.

1. BillFlow calculates worked minutes after Break.
2. Standard minutes are subtracted.
3. A candidate below Minimum overtime minutes becomes zero.
4. The remaining value is rounded down to the configured overtime interval.
5. An approver accepts the calculated overtime or approves zero overtime.
6. Payroll uses only Approved overtime minutes.

Example with a 480-minute standard day, 30-minute minimum, and 15-minute rounding:

```text
Worked time: 9 hours 8 minutes = 548 minutes
Candidate: 548 - 480 = 68 minutes
Approved calculation after rounding: 60 minutes
```

The employee must also be overtime-eligible in Compensation for overtime pay to be calculated in Payroll.

## Mark All Present

**Mark all present** is a data-entry shortcut. It:

- Changes editable Draft rows to Present.
- Uses the employee's default Shift or the first available Shift when blank.
- Uses the employee's default Work Location or the first available location when blank.
- Prefills Shift start, end, and break when a Shift is available.
- Marks the rows as changed.

It does not save, submit, or approve anything by itself. Review exceptions such as absences and leave before saving.

# Save and Approval Workflow

## Workflow Statuses

| Workflow | Meaning | Can edit? | Payroll eligible? |
| --- | --- | --- | --- |
| Draft | Work in progress | Yes, with Update permission | No |
| Submitted | Sent to an approver | No | No |
| Approved | Attendance and overtime accepted | Only after Reopen | Yes |
| Locked | Included in an approved payroll run | No | Yes, already tied to payroll |

## Save Draft

Use **Save** when entry is incomplete or still being checked.

- Only changed rows are saved.
- Incomplete working times may be kept as Draft.
- Saved Draft rows remain editable.
- A Draft does not affect payroll.

## Submit One Row

1. Save any unsaved changes first.
2. Select Submit on a Draft row.
3. Confirm the action.

Present and Half-Day rows need valid check-in/check-out data before submission. Submitted rows are read-only and wait for approval.

## Save and Submit a Batch

Use **Save & submit** to save eligible changed rows and submit the daily batch in one operation.

Before confirming, review:

- Number of employees included
- Present/Half-Day and absence/leave totals
- Rows with missing required working times
- Overtime candidate total

Rows that do not pass submission validation must be corrected.

## Approve One Row

An approver can approve a Submitted row. Approval confirms:

- Attendance status and payable day units
- Worked/regular minutes
- Approved overtime minutes
- Payroll eligibility

Use View before approval when the times or overtime need closer review.

## Save and Approve All

Users with Attendance **Approve** permission see **Save & approve all**. It can save eligible Draft data and move eligible Draft/Submitted rows directly to Approved.

The confirmation requires an overtime choice when the batch contains calculated overtime:

- Approve calculated overtime; or
- Approve attendance with zero overtime.

This shortcut is intended for an authorized supervisor or administrator who has reviewed the entire sheet. It should not be used merely to bypass the normal review process.

## Reopen Approved Attendance

Use Reopen when approved attendance needs correction before payroll locks it.

1. Select Reopen on the Approved row.
2. Enter the correction reason.
3. Confirm.
4. Correct the returned Draft.
5. Submit and approve it again.

The reason provides an audit trail. Current workflow supports reopening Approved attendance; review Submitted entries carefully because a Submitted row does not expose the same Reopen action.

## Locked Attendance

Attendance becomes Locked when an approved payroll run includes it. Locked records cannot be edited or reopened.

To correct a locked record:

1. Cancel related salary payments, if any.
2. Cancel the payroll run with a reason.
3. BillFlow returns the run's Locked attendance to Approved.
4. Reopen and correct the attendance.
5. Recalculate the payroll.

Do not cancel payroll casually; it reverses payroll accounting and advance recoveries.

# Attendance Register

## What Is It Used For?

The register is the searchable, server-paged history of saved attendance.

Typical columns include:

- Date
- Employee
- Attendance status
- Regular time
- Overtime candidate
- Approved overtime
- Workflow status
- Actions

Use shared table search, filters, sorting, print, Excel, and pagination. See [Navigation, Tables, and Common Actions](02-navigation-tables-and-common-actions.md).

Available actions follow the same View, Submit, Approve, and Reopen rules as Daily Entry.

# Monthly Report

## Filters

| Field | Required | Purpose |
| --- | --- | --- |
| Month | Yes | Reporting month |
| Department | No | Limits report to one department |

## Monthly Measures

- Present days
- Absent days
- Half days
- Paid leave
- Unpaid leave
- Week offs
- Holidays
- Payable days
- Regular worked hours
- Approved overtime hours
- Pending/unapproved records, where applicable

This report helps validate attendance before payroll. It is not a payslip and does not calculate salary amounts.

# Monthly Attendance Register

## What Is It Used For?

**Monthly register** is a print-style attendance sheet. It keeps one employee on each row and one column for every calendar day from 1 to 31, matching a conventional paper attendance register.

Use it when the business needs a month-wise attendance record that can be downloaded, printed, signed, or shared with payroll and management. It does not replace the existing Monthly Report; the Monthly Report remains the faster totals view.

## Register Filters

| Field | Required | Purpose |
| --- | --- | --- |
| Month | Yes | Calendar month shown in the register |
| Department | No | Shows employees from only one department |
| Payroll run | No | Adds rate, amount, advance, and balance columns from a payroll run covering exactly that calendar month |
| Approved only | No | Excludes Draft and Submitted attendance entries from the register |

Payroll run selection is shown only to users with Payroll access. Users without Payroll access can still create and export the attendance-only register.

## Attendance Codes

| Code | Meaning |
| --- | --- |
| P | Present |
| A | Absent |
| HD | Half Day |
| L | Paid Leave |
| UL | Unpaid Leave |
| WO | Weekly Off |
| H | Holiday |
| - | No attendance record saved for that date |

For months shorter than 31 days, the extra day cells remain blank and shaded. This preserves the standard register layout without suggesting that those dates exist.

## Payroll Columns

When a matching payroll run is selected, the register includes the payroll calculation already saved for each employee:

- **OT hours**: Approved overtime hours.
- **OT rate**: Hourly overtime rate used by payroll.
- **Total days**: Payroll payable-day units.
- **Rate**: Employee's saved daily wage or monthly salary rate.
- **Amount**: Gross payroll amount before deductions.
- **Advance**: Advance recovery included in the payroll calculation.
- **Balance**: Salary amount still unpaid after recorded salary payments.
- **Signature**: Blank column intended for a physical signature after printing.

Do not select a different-month payroll run. BillFlow only accepts a run whose start and end dates exactly match the selected calendar month.

## Download Excel

Select **Download Excel** after generating the register. The `.xlsx` file preserves:

- The company name and selected month heading.
- Employee identity columns and all 31 day columns.
- Colour-coded attendance codes and a code legend.
- Payroll summary and signature columns where payroll data is available.
- Frozen employee columns, repeatable header rows, borders, and landscape print settings for a wide attendance sheet.

## Permissions

| Task | Required Attendance permission |
| --- | --- |
| Open Daily Entry/Register/Report | List |
| View details | View |
| Create attendance | Insert |
| Edit/save/submit Draft attendance | Update |
| Approve, batch approve, or reopen | Approve |
| Print or Excel | Print or Export |

The exact action button appears only when the user's permission and the record status both allow it.

## Recommended Daily Process

1. Select the Work date and optional Department.
2. Use Mark all present only when it saves time.
3. Correct absences, leave, and half days.
4. Open Show all columns when Shift, Work Location, or Break needs review.
5. Verify times and overtime candidates.
6. Save Draft during entry.
7. Submit when complete.
8. Have an authorized user approve attendance and overtime.
9. Review the Monthly Report before creating payroll.
10. Generate the Monthly Register and download it when a printable attendance record is needed.

## Common Mistakes

- Assuming Save means Approved; Save creates or updates Draft attendance.
- Submitting before correcting Mark all present exceptions.
- Expecting hidden optional columns to be deleted.
- Entering check-out earlier than check-in by mistake and creating an overnight session.
- Entering Break longer than the work session.
- Treating calculated overtime as approved overtime.
- Approving overtime for an employee whose compensation is not overtime-eligible.
- Expecting Work Location to update Site Management.
- Leaving attendance Submitted or Draft and expecting Payroll to include it.
- Trying to edit Locked attendance without first cancelling the payroll run.

Continue with [Payroll](12-payroll.md).
