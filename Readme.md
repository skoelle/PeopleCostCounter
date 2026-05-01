# Meeting Cost Tracker

A small single-page tool that shows, in real time, how much a meeting is costing while it runs.

It is intentionally simple: enter how many developers are present, enter the average monthly gross salary, press **Start**, and the page begins counting the cost every second.

## What it calculates

The tracker estimates meeting cost from salary, employer overhead, team size, and elapsed time. The calculation is based on the idea that one developer’s salary can be converted into an annual employer cost, then into a working-hour and working-second cost. Similar meeting-cost tools commonly start from annual salary, convert it to an hourly rate, and multiply by meeting duration and headcount. [meetingtoll](https://www.meetingtoll.com/blog/meeting-cost-formula-per-employee)

## Formula

The app uses this formula:

\[
AnnualSalary = AvgMonthlySalary \times 12
\]

\[
AnnualSalaryWithEmployerContribution = AnnualSalary \times 1.2
\]

\[
TotalAnnualCost = AnnualSalaryWithEmployerContribution \times DevelopersPresent
\]

\[
CostPerSecond = \frac{TotalAnnualCost}{220 \times 8 \times 60 \times 60}
\]

The 1.2 multiplier is a simplified overhead factor for employer contributions, which is in the same rough range as public Germany payroll references that place employer burden around 20 to 23 percent above gross salary. [boundlesshq](https://boundlesshq.com/blog/payroll-in-germany/)

## Why 220 days

The app divides by 220 working days instead of 365 calendar days. That makes the result closer to actual working time, because meetings happen during paid work, not across the full calendar year. [capme](https://www.capme.app/meeting-cost-calculator)

Using 220 days, 8 hours per day, and 60 minutes per hour is a practical simplification that turns annual cost into a live per-second burn rate. It is not a payroll-grade accounting model, but it is a useful way to visualize meeting cost in real time. [meetingking](https://meetingking.com/meeting-cost-calculator/)

## Example

If 5 developers are present and the average monthly gross salary is 5,000 €:

- Annual salary per developer: 60,000 €
- Annual salary incl. employer contribution: 72,000 €
- Total annual cost for the meeting: 360,000 €
- Cost per second: about 0.0568 €
- Cost per minute: about 3.41 €
- Cost per hour: about 204.55 €

These numbers are consistent with the formula above.

## Controls

- **Start** begins the live counter at zero.
- **Reset** stops the counter and sets the accumulated cost back to zero.
- The cost per second is recalculated whenever the inputs change.
- The accumulated cost updates once per second while the counter is running.

## Notes

This tool is designed to make meeting costs visible, not to produce exact payroll accounting. In real companies, the true employer cost can vary by insurance rates, caps, bonuses, and other overhead, so the 1.2 factor should be understood as a simple approximation. [payrollgermany](https://payrollgermany.de/blog/employer-contributions-to-social-security-in-germany-a-comprehensive-guide/)

The result is best used as a conversation starter: it helps teams notice how quickly meeting time turns into money.