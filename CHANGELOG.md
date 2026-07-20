# CHANGELOG

Material structural and analytical changes, newest first.

## 2026-07-20 — Gate 6: historical reconciliation (cross-document verification)

- Executed the remaining `HISTORICAL_RECONCILIATION_PLAN.md` "Execution order at
  Gate 6" steps not already covered during extraction: cross-document GAAP
  statement checks (10-Q vs. same-quarter release) for all six quarters where
  both exist, cross-document balance-sheet checks (same six quarters plus
  FY25/FY26 Q4 release-vs-10-K), RPO footnote-vs-release checks for all eight
  quarters, and a bridge/L3 (CHECK_020) consolidation across all eight quarters.
- **Zero discrepancies found anywhere** — every cross-checked figure matches
  exactly between independently-transcribed sources.
- **C-07 (RPO series) RESOLVED**: full eight-quarter footnote-vs-release
  cross-check ties 8/8; cRPO recomputed for every quarter. Research Pack's
  FY24-inclusive series remains out of scope/unusable (Q-03).
- New file: `10_Working_Data/reconciliations/orcl_gate6_cross_document_checks.csv`
  (33 new checks, all pass) and `orcl_gate6_consolidated_dashboard.csv` (140-row
  merge of all three sessions' checks: 136 pass / 4 blocked / 0 fail).
- No architecture changes — pure verification pass, no field IDs/formulas/values
  added or changed. Created `00_project_control/GATE_6_REVIEW.md`.

## 2026-07-20 — Gate 5B: full historical extraction (FY2025 Q1 – FY2026 Q4)

- Extended the Gate 5A pilot's two-file pattern to the remaining six quarters
  (FY2025 Q1–Q4, FY2026 Q2–Q3), reusing the pilot's FY2026 Q1/Q4/annual values
  verbatim (no re-transcription). Combined total: 839 provenanced values (475
  reported / 256 calculated / 108 supplemental), 96 not-disclosed determinations.
- New files: `10_Working_Data/raw_extractions/orcl_historical_quarterly_full.csv`,
  `orcl_historical_quarterly_full_provenance.csv`,
  `orcl_fy2025_q4_derivation_support.csv`, `GATE_5B_EXTRACTION_LOG.md`;
  `10_Working_Data/reconciliations/orcl_historical_full_checks.csv`;
  `10_Working_Data/templates/orcl_historical_quarterly_template_v2.csv` (125-row,
  regenerated from the 137-field dictionary — original Gate 4 template untouched).
- 70 new reconciliation checks (69 pass, 1 blocked, 0 fail); combined with the
  Gate 5A pilot's 37 checks, 107 total checks run across both sessions, 103 pass /
  0 fail / 4 blocked. CHECK_050 sum-of-quarters now closes for both fiscal years
  across revenue, operating income, net income, depreciation, SBC, and cash flow.
- **D-016:** documented two disclosure-evolution findings — no dedicated lease
  supplemental footnote exists in the FY2025 Q1–Q3 10-Qs (BS_060/DEBT_050/
  DEBT_060 genuinely not disclosed those quarters, confirmed structural not an
  extraction gap); FY2025 exact-millions IaaS/SaaS dollars adopted from later
  FY26-release recast comparatives (precision upgrade over each period's own
  headline-billions disclosure). No field IDs changed.
- **D-017:** the new full-extraction file pair supersedes the pilot files as the
  Gate 6+ modeling input; pilot files retained unmodified as the Gate 5A audit
  trail.
- C-01 and C-02 quarterly series closed and tied to their FY25/FY26 annual anchors
  (Gate 5A had resolved only the annual figures); C-06 quarterly series confirmed
  as a routine, trackable disclosure across both years.
- Created `00_project_control/GATE_5B_REVIEW.md`. No source files in `01_`–`09_`
  modified; no AI-research values used (verified programmatically).

## 2026-07-20 — Gate 5A: historical extraction pilot (FY26 Q1 + FY26 Q4)

- Branch note: this session's designated branch
  `claude/oracle-historical-extraction-pilot-r6o3ov` was created from stale `main`;
  it was reset onto the prior working-branch tip `e06f7ae` (no unique commits lost —
  old tip was an ancestor) so all Gate 1–4 work and SRC-024 are included.
- Created `10_Working_Data/raw_extractions/` with the pilot value file
  (`orcl_historical_quarterly_pilot.csv`, template-shaped, 125 rows), a long-format
  per-value provenance file (249 values: 95 Q1, 95 Q4, 59 FY26-annual; 141 reported /
  66 calculated / 42 supplemental; 28 explicit not-disclosed rows),
  `orcl_fy2026_q4_derivation_support.csv` (44 FY-minus-9M derivations incl. 2 refusals
  for caption mismatch), and `PILOT_EXTRACTION_LOG.md`.
- Created `10_Working_Data/reconciliations/orcl_historical_pilot_checks.csv`
  (37 checks: 34 pass, 0 fail, 3 blocked-with-reason).
- Resolved **Q-18** (FY26 filed-statement reclassification confirmed), **C-01**
  (gross debt $129,541M; $135B claim = borrowings + preferred), **C-02** (FY26
  depreciation $7,623M), **C-06** ($260B uncommenced leases, off balance sheet,
  future-commitment treatment). Issued **Q-10** EBITDA recommendation
  (`11_Analysis/historical/EBITDA_DEFINITION_MEMO.md`), provisional pending user
  sign-off.
- Architecture (D-013/D-014/D-015): added 5 dual-presentation fields
  (REV_011/REV_021/REV_147/COGS_011/OPEX_065) to the data dictionary and source
  mapping (now 137 rows each, 1:1); amended the Layer 3 bridge for FY26 presentation;
  cleared stale "SRC-024 NOT YET RECEIVED" mapping annotations; matrix notes
  corrected (REV_120/130 footnote-level, DEBT_070/RPO_050 quarterly). Gate 4 template
  left untouched (regeneration deferred to Gate 5B).
- Manifest: capture-defect notes on SRC-013/SRC-016 (right-edge table clipping —
  FY26 quarterly supplemental columns missing from the Q4 release capture);
  SRC-024 marked extracted.
- Created `00_project_control/GATE_5A_PILOT_REVIEW.md`. No source files in `01_`–`09_`
  modified; no values taken from AI research reports (verified programmatically).

## 2026-07-20 — Branch sync: FY2026 10-K merged in and registered as SRC-024

- User committed `ORCL_2026_10-K_FY_Ended_2026-05-31.pdf` directly to `origin/main`
  (commit `d136102`, "Add files via upload").
- Merged `origin/main` into `claude/oracle-equity-model-mhmjq4` via a standard merge
  commit (no conflicts, no force-push, no history rewrite); all Gate 1–4 work confirmed
  intact post-merge.
- Verified filing identity (Form 10-K, Oracle Corporation, Commission File 001-35992,
  FYE 2026-05-31, signed 2026-06-22; 139 pages; no MD5 duplicate; not an LFS pointer).
- `git mv`'d it to `02_Annual_Filings/ORCL_2026_10-K_FY_Ended_2026-05-31.pdf`; registered
  as **SRC-024** in `source_manifest.csv`; replaced all `SRC-024_RESERVED` placeholders
  with `SRC-024` in `source_to_field_mapping.csv` (64 occurrences).
- Annotated C-01/C-02/C-06 and Q-01 to reflect source availability. **Did not** extract
  any figures or resolve any conflict — that remains Gate 5/6 work.

## 2026-07-20 — Gate 4: historical-data architecture

- Created `10_Working_Data/` (architecture, templates) and `11_Analysis/historical/`.
- Added the Gate 4 deliverable set: `HISTORICAL_DATA_ARCHITECTURE.md` (3-layer design),
  `orcl_data_dictionary.csv` (132 fields / 13 ID families), `source_to_field_mapping.csv`
  (132 rows, SRC-024 reserved for the missing FY26 10-K),
  `quarterly_disclosure_matrix.csv`, blank `orcl_historical_quarterly_template.csv`
  (120 rows), `HISTORICAL_RECONCILIATION_PLAN.md` (incl. YTD→standalone differencing
  spec), `EXTRACTION_PRECEDENCE_RULES.md`, `GATE_4_REVIEW.md`.
- Logged decisions D-009…D-012; opened Q-18; resolved Q-09; settled Q-03; annotated
  C-01/C-02/C-06 with designated resolution tests.
- No source files modified; no financial values extracted or entered anywhere.
- Note: FY26 10-K upload was attempted by the user but never reached the session
  filesystem — SRC-024 remains outstanding (Gate 5 scope B blocker).

## 2026-07-20 — Workspace organization (Gates 1–3)

- Adopted the numbered folder structure from `00_MASTER_CHECKLIST.md`; moved all 18 root
  PDFs into `02_`–`06_` folders and the two root research .docx files into
  `01_Research_Outputs/` (all via `git mv`; map in `00_project_control/PROPOSED_FILE_MOVE_MAP.md`).
- Renamed the two 10-K PDFs and the two research .docx files to project naming convention
  (dates verified from document contents).
- Created project governance set: root `CLAUDE.md`, `README.md`, `CURRENT_STATE.md`,
  `CHANGELOG.md`, `.gitignore`; `00_project_control/{project_scope, decision_log,
  open_questions, source_conflicts, SOURCE_INVENTORY_SUMMARY}.md`, `source_manifest.csv`,
  `PROPOSED_FILE_MOVE_MAP.md`.
- Registered 11 source conflicts (C-01…C-11) and 17 workspace questions (Q-01…Q-17);
  logged decisions D-001…D-008.
- No source-file contents modified; no files deleted; zero duplicates found.
