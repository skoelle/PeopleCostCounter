# AGENTS.md — PeopleCostCounter

This file guides future AI sessions and contributors working on this project.

## Project Overview

**PeopleCostCounter** ("Meeting Cost Tracker") is a tiny, self-contained, single-page HTML
app that calculates and displays — in real time — how much a meeting is costing while it
runs. It takes the number of developers present and the average monthly gross salary,
then counts up a running total cost once the user presses **Start**.

- **No build step.** Each `.html` file is a complete, standalone page.
- **No runtime dependencies.** Only vanilla HTML, CSS, and JavaScript.
- **No external JS libraries.** Google Fonts (Inter / JetBrains Mono) are loaded via CDN;
  pages work fine if fonts are blocked.
- **No persistence.** No localStorage, cookies, or server-side code.

## Project Structure

```
PeopleCostCounter/
├── LICENSE                          # MIT License
├── README.md                        # User-facing documentation
├── package.json                     # Dev tooling config (html-validate only)
├── .htmlvalidate.json               # HTML validation config/rules
├── screenshot.png                   # Promotional screenshot
├── meeting-cost-prompt.md           # Original development prompt / notes
├── meeting-tracker-de.html          # Canonical build — German UI
├── meeting-tracker-en.html          # Canonical build — English UI
├── .github/
│   └── workflows/
│       └── html-lint.yml            # CI: runs html-validate on push/PR
└── variants/
    ├── meeting-tracker-variant1.html  # Experimental — dark theme
    ├── meeting-tracker-variant2.html  # Experimental — dark gradient theme
    └── meeting-tracker-variant3.html  # Experimental — alternate styling
```

### Canonical vs. Variant Files

- `meeting-tracker-de.html` and `meeting-tracker-en.html` at the repository root are the
  **canonical builds**. Changes to the tracker should generally be applied to both.
- Files in `variants/` are **experimental or alternative designs** and may diverge from
  the canonical builds. Use them as a reference for styling ideas, but prefer editing the
  canonical files for functional changes.
- `meeting-cost-prompt.md` is an internal development artifact (the original prompt used to
  generate the tracker). It is not part of the public UI and can be referenced for
  context on design decisions and the cost formula.

## Cost Formula

```
AnnualSalary                = AvgMonthlySalary × 12
AnnualSalaryWithEmployer    = AnnualSalary × 1.2       # 20% employer overhead
TotalAnnualCost             = AnnualSalaryWithEmployer × DevelopersPresent
CostPerSecond               = TotalAnnualCost ÷ 220 ÷ 8 ÷ 60 ÷ 60
```

- **220 days** = approximate working days per year (accounts for weekends and holidays).
- **8 hours** = hours per working day.
- **1.2 multiplier** = simplified German employer contribution factor (~20%). This is an
  approximation, not payroll-grade accounting.
- See the README "What it calculates" section for full context and references.

### Test Values

| Developers | Monthly Salary | Cost/sec      | Cost after 60s |
|------------|----------------|---------------|-----------------|
| 8          | 5,000 €        | ~0.0909 €     | ~5.45 €         |

## Development Workflow

### Linting

HTML validation is performed with [html-validate](https://html-validate.org/).

```bash
# Install (creates node_modules)
npm install

# Lint all HTML files
npx html-validate "**/*.html"

# Via npm script
npm run lint:html
```

The CI workflow (`.github/workflows/html-lint.yml`) runs `npx html-validate "**/*.html"`
on every push and pull request targeting `main`. Ensure linting passes before committing.

### Local Preview

There is no dev server. Simply open any HTML file directly in a browser:

```bash
# Or use any static file server / Live Server extension
open meeting-tracker-en.html
```

### Adding Features or Fixing Bugs

1. Apply changes to **both** canonical files (`meeting-tracker-de.html` and
   `meeting-tracker-en.html`) to keep them in sync.
2. If the change is language-specific (e.g., German number formatting vs. English),
   update the relevant locale string only.
3. Run `npx html-validate "**/*.html"` to verify the HTML is still valid.
4. Test the cost calculation with the test values above.

### Branching Conventions

- Create branches named `feature/...` or `fix/...` for changes.
- Prefer small, focused pull requests.

## Code Conventions

### HTML Files

- Each source file begins with two license header comment lines:
  ```html
  <!-- Copyright (c) 2026 Stefan Koelle (https://stefankoelle.de) -->
  <!-- Licensed under the MIT License. See LICENSE file in project root for details. -->
  ```
- Inline CSS and JavaScript are used (no external `.css` or `.js` files) to keep each page
  fully self-contained.
- Inline styles are permitted (the `.htmlvalidate.json` config disables the
  `no-inline-style` rule).
- Semantic HTML is preferred: `<header>`, `<main>`, `<section>`, `<form>`, `<label>`,
  `<button>`, etc.
- Accessibility: buttons have `aria-label` attributes where the visual label is icon-only.
  SVG icons use `aria-hidden="true"`.

### JavaScript

- Vanilla JavaScript (no frameworks or libraries).
- The English (`meeting-tracker-en.html`) version includes a **theme toggle** (light/dark)
  and a **pause/resume** button.
- The German (`meeting-tracker-de.html`) version uses **Start/Reset** (no pause feature).
- Event handlers are attached via `onclick` in the HTML for buttons (e.g.,
  `onclick="handleBtn()"`).
- Number formatting uses `Intl.NumberFormat` with `de-DE` locale (German) or `en-GB` locale
  (English), both with `currency: 'EUR'`.
- The cost counter ticks via `setInterval` at 100ms for the running display and updates
  the per-second display on input change.

### CSS

- CSS custom properties (variables) are defined in `:root` for color palette, typography,
  spacing, and shadows.
- Both light and dark themes are supported via the `data-theme` attribute on `<html>`.
- Use `clamp()` for responsive font sizes where appropriate (e.g., the main cost display).

### `.htmlvalidate.json`

This file configures html-validate. The following rules are relaxed for this project:

| Rule                  | Setting | Reason                          |
|-----------------------|:-------:|----------------------------------|
| `no-implicit-button-type` | off | Buttons use default styling    |
| `no-inline-style`         | off | Inline styles are used throughout |
| `void-style`              | off | Mixed HTML5 void element styles   |
| `doctype-style`           | off | Mixed `<!DOCTYPE html>` and `<!doctype html>` |
| `aria-label-misuse`       | off | Lenient ARIA checking         |
| `no-redundant-aria-label` | off | Lenient ARIA checking         |

## Adding New Files

- Source code files should include the appropriate license header comment at the top.
- For HTML files:
  ```html
  <!-- Copyright (c) 2026 Stefan Koelle (https://stefankoelle.de) -->
  <!-- Licensed under the MIT License. See LICENSE file in project root for details. -->
  ```
- For files with a shebang line (e.g., Python `.py`), insert the license header **after**
  the shebang.
- Skip files that already contain the header.
- Markdown, JSON, package config files, and workflow files typically do not require headers.

## License

MIT License - Copyright (c) 2026 Stefan Koelle (https://stefankoelle.de)
- Full text in `LICENSE`
- License headers in all source code files
