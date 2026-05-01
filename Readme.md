# Meeting Cost Tracker

A small single-page tool that shows, in real time, how much a meeting is costing while it runs.

It is intentionally simple: enter how many developers are present, enter the average monthly gross salary, press **Start**, and the page begins counting the cost every second.

![Screenshot of the tracker](screenshot.png)

## Quick start

Open the tracker in your browser. The project is published via GitHub Pages — live demo URLs:

- English UI: https://skoelle.github.io/PeopleCostCounter/meeting-tracker-en.html
- German UI:  https://skoelle.github.io/PeopleCostCounter/meeting-tracker-de.html

You can also open the local HTML files directly in a browser (no build step required). Recommended browsers: Chrome, Edge, Firefox.

If you prefer a live-reload development workflow, use an editor extension such as Live Server (VS Code) or any simple static file server.

## Controls

- **Start** begins the live counter at zero.
- **Reset** stops the counter and sets the accumulated cost back to zero.
- The cost per second recalculates when inputs change; the accumulated cost updates once per second while running.

## Files of interest

- `meeting-tracker-variant1.html` — first variant (dark mode, shows annual totals after start)
- `meeting-tracker-variant2.html` — light-mode variant (recommended)
- `meeting-tracker-variant2-en.html` — English translation of variant 2
- `meeting-tracker-variant3.html` — alternate UI experiments
- `meeting-cost-prompt.md` — internal prompt and notes used while developing the tracker

## Browser & dependencies

- No build tool or runtime dependencies. The pages use only vanilla HTML/CSS/JS.
- Google Fonts are used for typography (Inter / JetBrains Mono); pages work fine if fonts are blocked.

## Example (quick test)

- Developers: `8`
- Avg. monthly: `5000`
- Expected: annual per-dev = `60.000 €`, incl. employer ≈ `72.000 €`, total for 8 ≈ `576.000 €`, cost/sec ≈ `0.0909 €`, after 60s ≈ `5,45 €`.

---

## What it calculates

The tracker estimates meeting cost from salary, employer overhead, team size, and elapsed time. The calculation is based on the idea that one developer’s salary can be converted into an annual employer cost, then into a working-hour and working-second cost. Similar meeting-cost tools commonly start from annual salary, convert it to an hourly rate, and multiply by meeting duration and headcount. [meetingtoll](https://www.meetingtoll.com/blog/meeting-cost-formula-per-employee)

### Formula

The app uses this formula:

```
AnnualSalary = AvgMonthlySalary × 12
AnnualSalaryWithEmployerContribution = AnnualSalary × 1.2
TotalAnnualCost = AnnualSalaryWithEmployerContribution × DevelopersPresent
CostPerSecond = TotalAnnualCost ÷ 220 ÷ 8 ÷ 60 ÷ 60
```

The 1.2 multiplier is a simplified overhead factor for employer contributions, which is in the same rough range as public Germany payroll references that place employer burden around 20–23% above gross salary. [boundlesshq](https://boundlesshq.com/blog/payroll-in-germany/)

### Why 220 days

The app divides by 220 working days instead of 365 calendar days. That makes the result closer to actual working time, because meetings happen during paid work, not across the full calendar year. [capme](https://www.capme.app/meeting-cost-calculator)

Using 220 days, 8 hours per day, and 60 minutes per hour is a practical simplification that turns annual cost into a live per-second burn rate. It is not a payroll-grade accounting model, but it is a useful way to visualize meeting cost in real time. [meetingking](https://meetingking.com/meeting-cost-calculator/)

## Notes

This tool is designed to make meeting costs visible, not to produce exact payroll accounting. In real companies, the true employer cost can vary by insurance rates, caps, bonuses, and other overhead, so the 1.2 factor should be understood as a simple approximation. [payrollgermany](https://payrollgermany.de/blog/employer-contributions-to-social-security-in-germany-a-comprehensive-guide/)

The result is best used as a conversation starter: it helps teams notice how quickly meeting time turns into money.

## Contributing

- Prefer small, focused pull requests. Create a branch named `feature/...` or `fix/...` for changes.
- If you want me to push changes, tell me whether to create a PR or commit directly to `main`.

## License

This repository does not yet include a LICENSE file. If you want a permissive license, I can add an `MIT` license file — tell me if that is acceptable or specify another license.

## Author / Contact

If you need changes, open an issue or contact the repository owner on GitHub.
