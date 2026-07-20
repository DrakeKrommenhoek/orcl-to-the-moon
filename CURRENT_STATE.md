# CURRENT_STATE

Last updated: 2026-07-20 (Gate 4 session — historical-data architecture)
Branch: `claude/oracle-equity-model-mhmjq4` (tracks origin; remote = DrakeKrommenhoek/orcl-to-the-moon)

## Current phase

**Gate 4 COMPLETE.** Gates 1–3 completed earlier on 2026-07-20. Next gate: **Gate 5
(data extraction)** — partially unblocked (see blockers).

## Completed work

- Gates 1–3: inventory, manifest (23 sources), duplicate review, conflict register
  (C-01…C-11), governance file set. See earlier section of this file's git history.
- Gate 4 (this session), no numerical extraction performed:
  - `11_Analysis/historical/HISTORICAL_DATA_ARCHITECTURE.md` — 3-layer design (L1 as
    filed / L2 explicit supplemental disclosures / L3 six-stream analytical + bridge)
  - `10_Working_Data/architecture/orcl_data_dictionary.csv` — 132 fields, 13 families,
    stable IDs (the script/Excel interface)
  - `10_Working_Data/architecture/source_to_field_mapping.csv` — 132 rows, 1:1 with
    dictionary; SRC-024 reserved for the FY26 10-K
  - `10_Working_Data/architecture/quarterly_disclosure_matrix.csv` — expected disclosure
    status per field per quarter (DR/DS/GR/CALC/YTD/ANN/EST/ND/TBD)
  - `10_Working_Data/templates/orcl_historical_quarterly_template.csv` — 120 extractable
    rows × 8 quarters + annual columns, empty by design
  - `11_Analysis/historical/HISTORICAL_RECONCILIATION_PLAN.md` — Gate 6 spec incl. YTD
    differencing formulas and check battery
  - `10_Working_Data/architecture/EXTRACTION_PRECEDENCE_RULES.md` — 9-rung ladder,
    12 handling rules
  - `00_project_control/GATE_4_REVIEW.md` — full gate review
  - Decisions D-009…D-012 logged; Q-18 opened; Q-09 resolved; Q-03 settled; C-01/02/06
    annotated with designated resolution tests

## Work in progress

None mid-flight. Clean stopping point.

## Known issues / blockers

1. **FY2026 10-K still missing (SRC-024 reserved).** An upload was attempted during the
   Gate 4 session but the file never reached the session filesystem. Re-provide it —
   most reliable: commit the PDF to `02_Annual_Filings/ORCL_2026_10-K_FY_Ended_2026-05-31.pdf`.
   Blocks: FY26 Q4/annual extraction, C-01/C-02/C-06 resolution, preferred terms (Q-11).
2. All 8 earnings-call transcripts missing (Q-04); analyst-day deck missing (Q-05).
3. User thesis template still blank (Q-06) — blocks Gate 8.
4. EBITDA definition undecided (Q-10) — PROF_160 computation blocked.
5. FY26 filed-statement presentation change unverified (Q-18) — first thing to check at
   Gate 5.
6. FactSet MCP connector present but unauthenticated (Q-08).

## Next recommended action

Gate 5, scope A (unblocked): extract FY25 Q1 – FY26 Q3 from 10-Qs + releases into the
template, plus FY26 Q4 release-level data; FY25 annual ties vs SRC-002. Scope B (blocked
until SRC-024): FY26 annual anchors, FY26 Q4 filing-grade validation, C-01/02/06
resolution. If SRC-024 has arrived: register it in the manifest first (identity check,
FYE 2026-05-31), then run full-scope Gate 5.

## Exact restart prompt for the next session (Gate 5)

> Read CLAUDE.md, CURRENT_STATE.md, and all of 00_project_control/ (especially
> GATE_4_REVIEW.md, open_questions.md, decision_log.md, source_conflicts.md), then
> 11_Analysis/historical/HISTORICAL_DATA_ARCHITECTURE.md, HISTORICAL_RECONCILIATION_PLAN.md,
> and 10_Working_Data/architecture/EXTRACTION_PRECEDENCE_RULES.md. If the FY26 10-K is
> now in 02_Annual_Filings/, validate its identity (Form 10-K, FYE 2026-05-31) and
> register it as SRC-024 in source_manifest.csv before anything else. Then execute Gate 5
> data extraction: populate 10_Working_Data/templates/orcl_historical_quarterly_template.csv
> (working copy in 10_Working_Data/raw_extractions/, template itself stays blank) for
> FY2025 Q1 – FY2026 Q4 following the three-layer rules, the precedence ladder, and
> blank-beats-guess (D-011). Resolve Q-18 (FY26 statement captions) first. Record source
> ID + section for every value; classify every cell reported/calculated; do not resolve
> conflicts without primary support; do not populate any Layer 3 stream except via the
> documented bridge; leave not-disclosed cells blank with status not_disclosed. Do not
> start Gate 6 reconciliation beyond the intra-document checks needed to trust the
> transcription; do not build the Excel model.

## Restart note

If this file and the architecture docs disagree, the architecture docs govern structure;
this file governs sequencing/status.
