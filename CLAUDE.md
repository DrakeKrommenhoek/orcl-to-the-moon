# CLAUDE.md — Oracle Equity Research Project

Operational rules for every Claude Code session in this repository. Project background
lives in `00_project_control/project_scope.md` — read it once; read this file always.

## Start-of-session procedure (mandatory)

1. Read `CURRENT_STATE.md` — current gate, work in progress, next action.
2. Read `00_project_control/open_questions.md` and `decision_log.md`.
3. Check `00_project_control/source_conflicts.md` before using any figure it lists.
4. Do not repeat completed gates or re-litigate logged decisions.

## Objective (one line)

Auditable eight-quarter Oracle operating forecast (FY27 Q1 – FY28 Q4) driving bear/base/bull
implied share prices at Oracle's next four earnings releases, via forward comparable-company
valuation with explicit financing, dilution, and capacity mechanics.

## Source-authority hierarchy (binding)

1. Oracle SEC filings (10-K, 10-Q, 8-K, prospectuses)
2. Oracle IR materials (earnings releases, slides, analyst day)
3. Peer official filings and IR materials
4. Earnings-call transcripts
5. Reputable financial press and market-data providers
6. ChatGPT/Gemini research reports (`01_Research_Outputs/`) — inputs and cross-checks only,
   never controlling. Known defects are catalogued in `source_conflicts.md`.
7. Unsourced assumptions — last resort, always labeled `assumed`

When sources disagree: record in `source_conflicts.md`; the higher-authority source wins
only after the conflict is documented.

## Folder conventions

Numbered structure (established by `00_MASTER_CHECKLIST.md`, extended this session):

- `00_project_control/` — governance: scope, decisions, questions, conflicts, manifest, move map
- `01_Research_Outputs/` — AI research + user thesis
- `02_Annual_Filings/` … `06_Financing_Capital_Structure/` — Oracle primary sources
- `07_Analyst_Day/`, `08_Earnings_Call_Transcripts/` — created when materials arrive
- `09_Comparable_Companies/` — peer materials
- Reserved, create only when the gate requiring them starts: `10_Working_Data/` (raw
  extractions, cleaned data, reconciliations, data dictionary), `11_Analysis/`,
  `12_Model/` (development, outputs, archived versions), `13_Deliverables/`, `99_Archive/`

File naming: `ORCL_<FYyyyy>_<Qn>_<DocType>_<date>.ext`, no spaces. New sources must be
added to `00_project_control/source_manifest.csv` on arrival.

## File-preservation rules (hard)

- **Never edit, convert-in-place, rename-without-move-map, or delete** anything in
  `01_`–`09_` source folders. Original sources are immutable.
- Extracted/cleaned versions go in `10_Working_Data/`, each linked back to its source
  file ID (SRC-###) from the manifest.
- Never delete duplicates on sight — report them in the move map first.
- Structural changes require an entry in `PROPOSED_FILE_MOVE_MAP.md` (or a successor map)
  and `CHANGELOG.md`, executed with `git mv`.

## Process gates (work in order, do not skip)

1 Folder inventory · 2 Source manifest · 3 Duplicate/conflict review · 4 Historical-data
architecture · 5 Data extraction · 6 Historical reconciliation · 7 Forecast-driver design ·
8 Scenario approval (**requires user sign-off + filled thesis doc**) · 9 Comps methodology ·
10 Minimal model build · 11 Model checks · 12 Full build · 13 Valuation · 14 Sensitivities ·
15 Investment interpretation.

Status of each gate is tracked in `CURRENT_STATE.md`. Gates 1–3 (organizational portion)
completed 2026-07-20.

## Data integrity (hard rules)

- **No fabricated data.** Never invent historicals, segment splits, consensus, multiples,
  dates, guidance, or prices. Unknown = blank + "unavailable/unresolved" label.
- Every hardcoded model input carries: source file ID, section/page, reporting period,
  publication date, market-data as-of date (if applicable), and a classification tag:
  `reported | guided | consensus | calculated | assumed`.
- Facts vs. assumptions are never mixed in one table without per-cell classification.
- Round-number quarterly OCI/SaaS series from AI reports are estimates, not disclosures
  (see conflict C-03) — rebuild from filings.

## Excel standards (for Gates 10+)

- Inputs, calculations, and outputs on separate tabs; single color convention for
  hardcodes vs. formulas vs. links; every hardcode cell traceable to the manifest.
- One scenario switch (bear/base/bull) driving all cases; no per-case copy-paste models.
- A dedicated checks tab: balance-sheet ties, cash-flow ties, revenue recast reconciles to
  reported categories, sum-of-quarters = fiscal year. Checks must be green before results
  are quoted.
- Model versions saved to `12_Model/archived_versions/` before material changes.

## Validation standards

- Extracted historicals are reconciled against a second source (release vs. 10-Q/10-K)
  before use (Gate 6).
- Derived Q4 figures (FY minus 9-month) are flagged `calculated`.
- Any figure that appears in `source_conflicts.md` is unusable until the conflict entry
  records a resolution.

## Session hygiene

- Update `CURRENT_STATE.md` at the end of every working session — no exceptions.
- Log material decisions in `00_project_control/decision_log.md`; log structural changes
  in `CHANGELOG.md`.
- Commit on the designated feature branch; never commit credentials, API keys, tokens, or
  `.env` files. Temp/scratch work stays out of the repo (see `.gitignore`).
