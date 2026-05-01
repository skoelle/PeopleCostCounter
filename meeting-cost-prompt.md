# Prompt: Meeting Cost Tracker — HTML App

Build a single, self-contained HTML page (no external dependencies except CDN fonts/icons) that calculates and displays the live running cost of a software engineering meeting.

---

## Layout & Inputs

On page load, show two input fields and two buttons:

- **Input 1** — Label: "Developers present", type: number, integer, min 1, no default value
- **Input 2** — Label: "Avg. monthly gross salary (€)", type: number, pre-filled with `5000`
- **Start button** — starts the cost counter from zero
- **Reset button** — stops the counter and resets the displayed cost back to zero; inputs remain editable

---

## Display

Below the inputs, show two display areas (visible at all times, initially showing zero):

1. **Large display — "Total cost so far"**
   - Updates every second while the counter is running
   - Shows the accumulated cost since Start was clicked
   - Format: German locale with 2 decimal places, e.g. `1.234,56 €`
   - This should be the visually dominant element on the page (large font, prominent placement)

2. **Smaller display — "Cost per second"**
   - Shows the calculated `CostPerSecond` value (static — only changes when inputs change)
   - Same number format: `0,03 €`

---

## Calculation

```
AnnualSalary            = AvgMonthlySalary × 12
AnnualSalaryWithEmployerContributions = AnnualSalary × 1.2
TotalAnnualCost         = AnnualSalaryWithEmployerContributions × DevelopersPresent
CostPerSecond           = TotalAnnualCost ÷ 220 days ÷ 8 hours ÷ 60 minutes ÷ 60 seconds
```

> **Note on 220 days:** This uses 220 working days per year (accounts for weekends and public holidays), not 365 calendar days — this gives a more accurate cost-per-working-second figure.

The `CostPerSecond` value must be recalculated whenever the inputs change. If the counter is running while the user changes an input, the new rate applies immediately to subsequent seconds.

---

## Button Behavior

- **Start**: Begins the interval counter (1-second tick). Disabled while counter is running.
- **Reset**: Stops the counter, sets accumulated cost display back to `0,00 €`, re-enables the Start button.
- There is no Pause. Reset is the only way to stop the counter.

---

## Validation

Before starting the counter, validate:
- "Developers present" must be a whole number ≥ 1
- "Avg. monthly gross salary" must be > 0
- Show a clear inline error message if validation fails; do not start the counter

---

## Design & UX

- Single-page, fully self-contained HTML file
- No frameworks required — vanilla HTML, CSS, JS is preferred
- Clean, modern dark UI — this will be used on a screen during internal meetings
- The "Total cost so far" number should be the largest visual element on the page — make it dramatic and easy to read from across a room
- The page should work well at 1080p (1920×1080) full-screen in a browser
- Include a subtle visual indicator (e.g. pulsing dot or color change) when the counter is actively running
- No localStorage, no cookies, no server-side code

---

## Example Values (for testing)

- 8 developers, €5,000 avg salary
- AnnualSalary = 60,000 €
- AnnualSalaryWithEmployerContributions = 72,000 €
- TotalAnnualCost = 576,000 €
- CostPerSecond = 576,000 ÷ 220 ÷ 8 ÷ 3,600 ≈ **0.0909 €/sec**
- After 60 seconds: ≈ 5,45 €
