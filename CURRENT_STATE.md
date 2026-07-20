# CURRENT_STATE

Last updated: 2026-07-20 (organizational pass, first Claude Code session on this repo)
Branch: `claude/oracle-equity-model-mhmjq4`

## Current phase

**Gates 1–3 complete (organizational portion).** Gate 4 (historical-data architecture)
not started. Numeric conflict resolution deferred to Gates 5–6 by design.

## Completed work

- Full workspace inventory; all 23 files opened and verified against their filenames
  (PDF page-1 checks, MD5 duplicate scan — zero duplicates).
- Repository reorganized into the checklist's numbered structure via `git mv` (no
  content changes, no deletions). Audit trail: `00_project_control/PROPOSED_FILE_MOVE_MAP.md`.
- Created: `CLAUDE.md`, `README.md`, `CURRENT_STATE.md`, `CHANGELOG.md`, `.gitignore`,
  and in `00_project_control/`: `project_scope.md`, `source_manifest.csv`,
  `SOURCE_INVENTORY_SUMMARY.md`, `source_conflicts.md` (11 conflicts C-01…C-11),
  `open_questions.md` (Q-01…Q-17 + Framework §16 list), `decision_log.md` (D-001…D-008),
  `PROPOSED_FILE_MOVE_MAP.md`.
- Both AI research documents read in full and characterized; their known defects are
  registered as conflicts.

## Work in progress

None mid-flight. Clean stopping point.

## Key decisions made (full text in decision_log.md)

Checklist folder structure adopted (D-001); git-mv-only reorganization (D-002/003);
AI-report OCI/SaaS quarterly splits demoted to estimates (D-005); manifest keyed by
SRC-### IDs (D-006); git strategy set, LFS deferred (D-007).

## Known issues / blockers

1. **FY2026 10-K missing** — controlling source; blocks C-01/C-02/C-06 resolution (user
   must download; sandbox cannot reach sec.gov — URLs in `00_project_control/00_MASTER_CHECKLIST.md`).
2. All 8 earnings-call transcripts missing; 2025 Analyst Day deck missing.
3. User thesis template (`01_Research_Outputs/ORCL_User_Thesis_and_Questions.docx`) is blank
   — blocks Gate 8 scenario approval and instrument choice.
4. Research Pack contains internally inconsistent FY26 revenue rows and unlabeled
   estimates — do not extract from it (C-03/C-04/C-08).
5. Comp market data single-sourced, as-of 2026-07-17/20, will be stale by first valuation
   date (C-09).
6. FactSet MCP connector present but unauthenticated (candidate consensus source, Q-08).

## Next recommended action

1. User: drop in FY26 10-K (+ transcripts, analyst-day deck if available) and fill the
   thesis template.
2. Claude: register new arrivals in the manifest, then run **Gate 4** — design the
   historical-data architecture (schema for the six-stream quarterly recast FY25 Q1 –
   FY26 Q4, data dictionary, reconciliation plan) in `10_Working_Data/data_dictionary/`.
   Gate 4 can start even before the 10-K arrives; Gate 5 extraction should wait for it.

## Exact restart prompt for the next session

> Read CLAUDE.md, CURRENT_STATE.md, and the files in 00_project_control/ (especially
> open_questions.md, decision_log.md, source_conflicts.md). Register any newly added
> source files in source_manifest.csv per D-006. Then execute Gate 4: propose the
> historical-data architecture — quarterly recast schema (six revenue streams per D-005/
> Q-09), field-level data dictionary, source-to-field mapping using SRC IDs, and the
> Gate 6 reconciliation plan. Do not extract numbers yet and do not modify any file in
> 01_–09_. If the FY26 10-K has been added, prioritize planning C-01/C-02/C-06 resolution.
