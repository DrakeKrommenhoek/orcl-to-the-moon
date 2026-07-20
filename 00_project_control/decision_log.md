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

## D-013 · 2026-07-20 · Dual-presentation Layer 1 for the FY26 reclassification (Q-18)
Oracle's FY26 filings reclassify the filed income statement (Cloud/Software captions,
"Cloud and software" expense relabel, 10-K-level "Restructuring and other" merge,
preferred-dividend EPS mechanics). Rather than redefining existing fields, five fields
were added — REV_011 (Cloud, as filed FY26), REV_021 (Software, as filed FY26),
REV_147 (Software license, by offerings), COGS_011 (Cloud and software expenses),
OPEX_065 (Restructuring and other, combined caption) — and the Layer 3 bridge was
amended for FY26-presentation periods: REV_330 = REV_145 (software support is now
directly disclosed, no residual), REV_340 = REV_147. Pre-FY26 fields (REV_010/020,
COGS_010, REV_140) stay defined as-was and are `not_disclosed` from FY26 Q1. Each
period is stored exactly as filed; the recast comparatives in FY26 filings are the
documented bridge (they tie exactly). Field IDs remain stable; no extracted value was
ever redefined. Dictionary/mapping updated to 137 rows; template regeneration deferred
to Gate 5B start (original Gate 4 template preserved unchanged).

## D-014 · 2026-07-20 · EBITDA definition (provisional — awaiting user ratification, Q-10)
Primary historical EBITDA (PROF_160) = GAAP operating income (PROF_010) + cash-flow-
statement depreciation (PROF_140) + amortization of intangibles (CF basis). SBC is NOT
added back; restructuring/acquisition costs stay in (a separate "adjusted EBITDA"
series may add them back at Gate 13); operating-lease expense stays in (EBITDA, not
EBITDAR — consistent with borrowings-only gross debt per C-01); one-time investment
gains (Ampere, Bloom) are excluded by construction because they sit below operating
income. Cross-check series: non-GAAP operating income + depreciation. FY26 values:
primary 29,900; NI-up variant 33,447; non-GAAP variant 36,549 — materially different,
never interchangeable. Full memo: 11_Analysis/historical/EBITDA_DEFINITION_MEMO.md.
Provisional until the user signs off; PROF_160 values are labeled accordingly.

## D-015 · 2026-07-20 · Q4 value precedence and pilot provenance format
(a) Where the Q4 release directly discloses a standalone Q4 statement line, the release
value is stored as `reported` and the FY-minus-9M derivation is the validation (five
lines differ by exactly $1M due to recast rounding — documented, within tolerance).
Where no direct Q4 disclosure exists (cash flows, depreciation, interest income,
by-offerings sub-streams), the FY−9M value is stored as `calculated` with both source
citations. Derivations are refused where FY and 9M captions are inconsistent (CF_040
acquisitions; CP vs short-term-financing split) — those cells are `not_disclosed`.
(b) The template-shaped extraction file cannot carry per-cell provenance, so the pilot
introduces a companion long-format file (`orcl_historical_quarterly_pilot_provenance.csv`,
one row per populated value with source ID/filename/section/classification/GAAP-tag/
formula/precision/status/notes). This two-file pattern is the standard for Gate 5B.
