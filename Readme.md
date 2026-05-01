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

## Quick start

To open the tracker locally you don't need a build step — just open one of the HTML files in a modern browser (Chrome, Edge, Firefox). For example:

- Open `meeting-tracker-en.html` in a browser for the light-themed, feature-complete UI.
- Open `meeting-tracker-de.html` for the german UI.

If you prefer a live-reload development workflow, use an editor extension such as Live Server (VS Code) or any simple static file server.

## Files of interest

- `meeting-tracker-variant1.html` — first variant (dark mode, shows annual totals after start)
- `meeting-tracker-variant2.html` — light-mode variant (no auto-start, shows annual / employer / total tiles)
- `meeting-tracker-variant2-en.html` — English translation of variant 2
- `meeting-tracker-variant3.html` — alternate UI experiments
- `meeting-tracker-de.html` / `meeting-tracker-en.html` — other language variants
- `meeting-cost-prompt.md` — internal prompt and notes used while developing the tracker

## Browser & dependencies

- No build tool or runtime dependencies. The pages use only vanilla HTML/CSS/JS.
- A Google Fonts CDN is used for typography (Inter / JetBrains Mono); the pages work fine if fonts are blocked.

## Example (quick test)

- Developers: `8`
- Avg. monthly: `5000`
- Expected: annual per-dev = `60.000 €`, incl. employer ≈ `72.000 €`, total for 8 ≈ `576.000 €`, cost/sec ≈ `0.0909 €`, after 60s ≈ `5,45 €`.

## Contributing

- Prefer small, focused pull requests. Create a branch named `feature/...` or `fix/...` for changes.
- If you want me to push changes, tell me whether to create a PR or commit directly to `main`.

## License

This repository does not yet include a LICENSE file. If you want a permissive license, I can add an `MIT` license file — tell me if that is acceptable or specify another license.

## Author / Contact

If you need changes, open an issue or contact the repository owner on GitHub.
