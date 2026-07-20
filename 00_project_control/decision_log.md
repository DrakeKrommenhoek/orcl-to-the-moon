# Decision Log

Decisions are numbered, dated, and never silently reversed — a reversal is a new entry.
Unresolved items belong in `open_questions.md`, not here.

## D-001 · 2026-07-20 · Adopt the checklist's numbered folder structure
The prior session's `00_MASTER_CHECKLIST.md` layout (`01_`–`09_` source folders) is
adopted as canonical rather than replaced, because it is intentional, logical, and the
downloaded filenames already match it. Extended with `00_project_control/` now and
reserved numbers `10_`–`13_` + `99_Archive/` for later gates. Empty folders are not
created in advance.

## D-002 · 2026-07-20 · Reorganization executed via git mv only
All file moves/renames per `PROPOSED_FILE_MOVE_MAP.md` were executed with `git mv`
(history-preserving, reversible). No source file content was modified. No files deleted.

## D-003 · 2026-07-20 · 10-K renames to checklist convention
`Oracle 2024 10K.pdf` and `Oracle 2025 10K.pdf` renamed to the checklist's exact target
names after verifying fiscal-year-end dates on page 1 of each PDF.

## D-004 · 2026-07-20 · AI research .docx files treated as the expected deep-research deliverables
The two root .docx files (Research Pack, Eight-Quarter Framework) are filed in
`01_Research_Outputs/` with dated ORCL-prefixed names, presumed to be the
ChatGPT/Gemini deliverables from the checklist (same 2026-07-20 date). Provider
attribution left open (Q-02). Both carry authority rank 6 regardless of provider.

## D-005 · 2026-07-20 · AI-report quarterly OCI/SaaS splits classified as estimates
Round-number quarterly OCI/SaaS revenue series in the Research Pack are classified as
research estimates, not disclosures (conflict C-03). The historical OCI/apps split will
be rebuilt from primary sources during extraction; where Oracle disclosure is
insufficient, the split will be labeled `calculated`/`assumed` with method notes.

## D-006 · 2026-07-20 · Source manifest is append-only and keyed by SRC-### IDs
Every future source file gets a manifest row on arrival; model inputs cite SRC IDs.

## D-007 · 2026-07-20 · Git strategy
Repository stays git-tracked including source PDFs (~50 MB total, stable, append-mostly).
`.gitignore` added for temp/derived/credential files. Git LFS deferred unless the repo
approaches ~1 GB or per-file 50 MB+ (Q-16). Work proceeds on branch
`claude/oracle-equity-model-mhmjq4`.

## D-008 · 2026-07-20 · Gate 1–3 (organizational portion) declared complete
Inventory, manifest, duplicate review (none found), and conflict register are done.
Numeric conflict *resolution* (C-01…C-11) is explicitly deferred to Gates 5–6.

## D-009 · 2026-07-20 · Three-layer historical architecture
Layer 1 = statements exactly as filed; Layer 2 = explicitly disclosed supplemental
metrics (release/slides/MD&A/footnotes) at disclosed precision; Layer 3 = six-stream
analytical architecture populated historically only through the documented bridge in
`HISTORICAL_DATA_ARCHITECTURE.md` §7. AI-report estimates can satisfy no layer.

## D-010 · 2026-07-20 · YTD cash-flow handling fixed
10-Q cash-flow figures stored as-filed (YTD) in dedicated fields; standalone quarters
exist only as calculated fields via Q1=YTD1, Q2=YTD2−YTD1, Q3=YTD3−YTD2, Q4=FY−YTD3,
with the validation battery in `HISTORICAL_RECONCILIATION_PLAN.md` §15.

## D-011 · 2026-07-20 · Blank-beats-guess extraction rule
Where rungs 1–6 of the precedence ladder disclose nothing, the historical cell stays
blank with status `not_disclosed`. Rounded disclosures keep stated precision. AI research
reports are barred from supplying any historical financial value (implements C-03/C-04/
C-08; extends D-005).

## D-012 · 2026-07-20 · Stable field-ID interface
132 fields across 13 families (REV_, COGS_, OPEX_, PROF_, CF_, BS_, DEBT_, SHARE_, KPI_,
RPO_, CAP_, VAL_, CHECK_) in `orcl_data_dictionary.csv`. Field IDs are permanent; scripts
and spreadsheets reference IDs, never labels. ID gaps (10s) allow insertion without
renumbering.
