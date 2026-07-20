# CHANGELOG

Material structural and analytical changes, newest first.

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
