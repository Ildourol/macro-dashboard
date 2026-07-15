# Project History And Change Commitments

This file is the offline project memory for `C:\Users\Admin\Downloads\macro-dashboard`.
It exists so the dashboard can stand alone without relying on chat history.

Every requested change that is implemented in this project must be recorded here, or in
`instructions.md` when it changes operating rules. Prefer recording both when the change
affects future maintenance.

## Standing Commitments

- Keep the dashboard runnable from `C:\Users\Admin\Downloads\macro-dashboard` without
  needing the original chat.
- Keep source dates separate from download dates.
- Keep calculations auditable in `instructions.md`.
- Keep online source URLs and offline fallback locations documented.
- Keep copied skills in `skills/` available as local methodology references.
- After any structural change, run `verify.cmd`.
- After any source refresh, record what changed, what failed, and what remains stale.
- Do not reintroduce retired split pages into top navigation unless explicitly requested.
- If a user asks for a new source, page merge, calculation, or report workflow, update
  this file with the request and update `instructions.md` if it changes repeat behavior.

## Change Log

### 2026-07-06 - Full Data Refresh + Volatility Calc Correction

- Request: "update the dashboard with the latest files, redo the calculations and the
  analysis. pull all the data and macro research."
- Data pulled: re-downloaded the CME/strategy PDF pack via BITS (57 files OK; Insider Week
  HTML snapshots 404 as usual — gated). Re-verified every cross-asset level against the
  live FMP MCP feed (indexes, UST curve, VIX, commodities, crypto, FX), pulled CFTC COT
  (ES), the economic calendar (07/06–07/17), sector performance, and re-checked the
  Merrill/Ameriprise/FactSet PDFs. **Trade date is still Thu 07/02** (markets closed 07/03;
  07/06 not settled), so CME PDFs and cash-index closes are byte-identical/unchanged — the
  new material is verified levels, a live 07/06 overlay, and rebuilt calculations.
- Calculations redone: pulled ~30 daily S&P closes and recomputed realized vol on 10-day
  (12.3%) and ~4-week (15.4%) windows. **This corrects the previously stored 6-observation
  ~8.5% RV, which had overstated the variance-risk premium.** VRP goes from "+7.3 rich" to
  fair-to-thin (+3.6 / +0.4; live +1.0). Confirmed curve spreads (2s10s +35, 3m10y +67,
  bear-steepener), SOFR strip (+31bp priced, unchanged), and sizing.
- Analysis updated: `risk-lab.html` (VRP section + chartVRP fully rebuilt, volatility
  regime), `quant-framework.html` (signal-stack VRP row), `playbook.html` (conviction,
  primary risk, 07/06 refresh confirmation), `index.html` (refresh banner, snapshot cards,
  live overlay, footer), `rates.html` (typo fix + live read), `calendar.html` (econ
  forecasts: ISM, FOMC Minutes 07/08, CPI 3.9%/core 2.8%, PPI 0.8%, Retail Sales),
  `cot.html` (CFTC 06/23 cross-check — matches Insider Week exactly), `strategists.html`
  (dates; Ameriprise still stale 06/15), `fx.html` and `futures-setups.html` (live overlays),
  `source-ledger.html` (freshness dates + live-feed and CFTC rows).
- Verification: `dashboard.ps1 verify` passes (sections balanced, nav present); all edited
  pages serve HTTP 200 via serve.ps1.
- Caveat for future agents: the FMP / Alpha-Vantage / FMP-COT MCP servers are this
  timeline's authoritative price universe (S&P ~7,483, gold ~4,162) — do NOT use WebSearch
  for prices; real-world 2026 figures belong to a different universe and will corrupt the
  dashboard. Gamma level still needs a fresh browser capture.

### 2026-07-05 - Standalone Dashboard Hardening

- Added `instructions.md` as the standalone operating manual for the multi-page HTML
  dashboard.
- Copied a portable `skills/` pack into the dashboard folder, including Codex profile
  skills, plugin/cache skills, custom dashboard skills, and the local Claude runner skill.
- Added offline CME PDFs, source snapshots, Insider Week graph snapshots, and refresh
  manifests as auditable local source material.
- Added source-refresh rules: source-displayed dates outrank download dates, blocked
  sources require browser capture or stale labeling, and live values should not be
  invented from memory.
- Added calculation recipes for futures risk sizing, pivots, SOFR implied rates, VRP,
  COT/TFF nets, breadth ratios, GuruFocus premium, composite ranking, and Kelly sanity
  checks.
- Merged dashboard pages according to the current project structure:
  Source Ledger & Snapshots, Market Lab & GuruFocus, Index & Operations, Playbook &
  Bottom Line, Quant Framework, and Executive Risk Lab.
- Revamped COT sources to Insider Week, including percentage heatmap values, TFF rows,
  and graph snapshots.
- Added Barron's U.S. index table to the home page.

### 2026-07-05 - Offline History Rule

- Added this `HISTORY.md` file as the local change memory.
- Updated `instructions.md` so every future requested change must also update
  `HISTORY.md` or the instruction file when repeat behavior changes.
- Updated verification so `HISTORY.md` is treated as a required standalone file.

### 2026-07-05 - Attached Market Research Bookmark Catalog Added

- Request: Use the attached Market Research bookmarks list as the available source-link
  inventory, update the standalone dashboard and report projects, and make future source
  checks/downloads independent of chat history.
- Changed: Added `sources\source-catalog.md`, `sources\source-map.md`, and
  `sources\market-research-bookmarks-pasted-text.txt`; updated `instructions.md`,
  `README-DASHBOARD.txt`, `source-ledger.html`, and `tools\dashboard.ps1`.
- Sources/calculations/skills: Added source catalog groups for market research PDFs,
  CME daily reports, CME daily bulletin section PDFs, CME monthly reports, insight pages,
  COT/TFF, gamma, Barchart cheat sheets, and StockAIO pivots. Applied the
  `market-data-connectors` workflow for source selection, freshness checks, and caveats.
- Verification: Run `verify.cmd` after this change.
- Caveats: Automatic bulk downloading was not added because several sources are
  paywalled, licensed, JavaScript-rendered, or better handled by browser capture.
