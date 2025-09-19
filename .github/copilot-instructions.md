# Copilot instructions — canada-tax-optimizer

This repository is a single-file web app (`код_веб_приложения_canada_tax_optimizer.html`) that implements a Canada tax comparison/optimizer UI and calculation engine in plain HTML+JS. The guidance below helps an AI code assistant be productive quickly.

Key facts (big picture)
- Single-file app: UI, data, logic, and styles are all inside `код_веб_приложения_canada_tax_optimizer.html`.
- Calculation core lives in JS functions near the bottom: `taxProgressive`, `ohpOnt`, `computeA`, `computeB`, `computeC`, `computeD`.
- Data-driven definitions: `STRUCTURES`, `LABEL_MAP`, `SOURCES`, and `ABBR` drive the scenario list and tooltips.
- Small DOM rendering layer: `renderFormsList()` constructs table rows from `STRUCTURES` and `SOURCES`. `selfTests()` performs lightweight runtime assertions.

What to edit and how
- Prefer targeted edits to the single HTML file (do not split into many smaller files unless user asks). Keep markup, styles, and logic grouped to preserve the app's single-file nature.
- When changing tax logic, update both the functions (e.g., `taxProgressive`) and corresponding `selfTests()` assertions if behavior/columns change.
- If you add new scenario items, update `STRUCTURES` (top-level) and `SOURCES` (for links/quotes). Use the same object shape (id, title, desc, src).

Conventions & patterns to follow
- Currency/percent formatting: uses `Intl.NumberFormat('en-CA', ...)` patterns at the top of the script (`fmtC`, `fmtP`). Reuse these when printing numbers.
- Sticky table columns: first two columns are intentionally sticky with CSS classes `col-fixed1` and `col-fixed2`; preserve these when changing table markup.
- IDs and element hooks: main hooks are `provSel`, `formsListBody`, `topAmount`, `topCalc`, `structSel`. Use these IDs for event wiring.
- Language: UI text is in Russian; preserve or mirror translations when adding UI strings unless asked to change locale.

Developer workflows
- No build system; open the HTML file in a browser to run. For quick iteration, use a local static server (examples):
  - Python: `python -m http.server 8000` (from repo folder) then open `http://localhost:8000/код_веб_приложения_canada_tax_optimizer.html`.
  - Live reload: use your editor's Live Server extension if available.
- Quick smoke tests: open devtools Console — `selfTests()` runs on DOMContentLoaded and logs assertions. Use `renderFormsList()` manually after edits to re-render.

Integration points & external dependencies
- No npm/node dependencies; external links are only documentation references in `SOURCES` pointing to CRA and provincial docs.
- All data and logic are client-side; there are no network calls or APIs to mock.

Examples to reference
- To change progressive tax bands: edit `state.fed` and `state.prov.ON` arrays near the top of the script and re-run `renderFormsList()`.
- To add a scenario: append an object into `STRUCTURES` with the same fields (title, desc, cat) and add any supporting `SOURCES[title]` entries.
- To alter OHP logic: edit `ohpOnt(taxable)` — it is a piecewise function with capped increments; tests rely on approximate thresholds.

Testing & safety
- Keep `selfTests()` assertions or extend them when adding columns/rows. They are lightweight and provide immediate feedback in the console.
- Avoid blocking the UI with heavy synchronous computations — if adding heavier simulations, move them behind a button and consider `setTimeout` or Web Worker.

If you need more
- Ask for intended scope: (refactor into modules, add build/test infra, add localization, or add export/import features). I will update this file accordingly.

---
Please review sections that are unclear or missing (e.g., intended language changes or plans to split the app). I'll iterate quickly.
