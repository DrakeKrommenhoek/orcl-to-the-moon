# Oracle (ORCL) Equity Research & Valuation Model

An auditable equity-research workspace for building an eight-quarter Oracle operating
forecast (FY27 Q1 – FY28 Q4) and bear/base/bull implied share prices at Oracle's next
four earnings releases, using forward comparable-company valuation with explicit
capacity, financing, and dilution mechanics.

## How a new session should begin

1. Read `CLAUDE.md` (operational rules — binding).
2. Read `CURRENT_STATE.md` (current gate, next action, restart instructions).
3. Read `00_project_control/open_questions.md`, `decision_log.md`, `source_conflicts.md`.
4. Continue from the gate recorded in `CURRENT_STATE.md`. Do not skip gates.

## Folder map

| Folder | Contents |
| --- | --- |
| `00_project_control/` | Governance: scope, master checklist, source manifest, inventory summary, move map, conflicts, open questions, decision log |
| `01_Research_Outputs/` | AI deep-research reports (rank-6 inputs, never controlling) + user thesis template |
| `02_Annual_Filings/` | Oracle 10-Ks (FY2024, FY2025; **FY2026 still missing — top acquisition priority**) |
| `03_Quarterly_Filings/` | Oracle 10-Qs (FY25 Q1–Q3, FY26 Q1–Q3) |
| `04_Earnings_Releases/` | Eight releases, FY25 Q1 – FY26 Q4 |
| `05_Earnings_Slides/` | FY26 Q4 deck (treat as primary modeling source) |
| `06_Financing_Capital_Structure/` | CY2026 equity & debt financing plan announcement |
| `07_Analyst_Day/`, `08_Earnings_Call_Transcripts/` | Not yet created — materials missing (see inventory summary) |
| `09_Comparable_Companies/` | Peer source index (MSFT, AMZN, GOOGL, SAP, CRM, NOW, IBM, CRWV) |
| `10_Working_Data/` … `13_Deliverables/`, `99_Archive/` | Reserved; created when their process gate starts |

## Controlling files

- **Source of truth for facts:** files in `02_`–`06_` (Oracle SEC/IR documents), per the
  authority hierarchy in `CLAUDE.md`. Original sources are immutable.
- **Source of truth for process:** `CLAUDE.md` + `00_project_control/` files.
- **Source registry:** `00_project_control/source_manifest.csv` (every source has an
  SRC-### ID; model inputs cite these IDs).

## Where final outputs will live

- Excel model: `12_Model/` (development / outputs / archived_versions)
- Price-target and investment memos, charts: `13_Deliverables/`

## Version control

Git repo; work happens on `claude/oracle-equity-model-mhmjq4`. Source PDFs are tracked
(stable, ~50 MB). Ignored: temp/lock files, caches, extraction scratch, `.env`/credentials
(never commit these). Revisit Git LFS only if the repo approaches ~1 GB.

## Status

Gates 1–3 (inventory, manifest, duplicate/conflict review) completed 2026-07-20.
Next: acquire missing sources (FY26 10-K above all), then Gate 4 (historical-data
architecture). Details in `CURRENT_STATE.md`.
