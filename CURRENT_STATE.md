# CURRENT_STATE

Last updated: 2026-07-20 (Gate 5B full extraction session)
Branch: `claude/oracle-historical-extraction-pilot-r6o3ov` (reset onto prior tip
`e06f7ae` of `claude/oracle-equity-model-mhmjq4`; remote = DrakeKrommenhoek/orcl-to-the-moon)

## Current phase

**Gate 5B (full historical extraction) COMPLETE.** Gates 1–4 and the Gate 5A pilot
completed earlier on 2026-07-20. All eight historical quarters (FY2025 Q1 – FY2026
Q4) plus both fiscal-year annual anchors are now extracted, provenanced, and
checked. **Next: Gate 6 (historical reconciliation, cross-document checks).**

## Completed work

- Gates 1–3: inventory, manifest (24 sources), duplicate review, conflict register.
- Gate 4: three-layer architecture, data dictionary, mapping, matrix, template,
  reconciliation plan, precedence rules.
- Branch-sync: FY2026 10-K registered as SRC-024.
- **Gate 5A (pilot):** FY2026 Q1 + Q4 proof-of-concept — 249 values, 37 checks
  (34 pass), resolved Q-18/C-01/C-02/C-06, issued Q-10 EBITDA recommendation
  (D-014, provisional), added D-013 dual-presentation fields. See
  `GATE_5A_PILOT_REVIEW.md`.
- **Gate 5B (this session): full eight-quarter extraction.**
  - Extended the pilot's two-file pattern to FY2025 Q1–Q4 and FY2026 Q2–Q3.
    Combined total: **839 populated values** (475 reported / 256 calculated / 108
    supplemental), **96 not-disclosed determinations**, across all 8 quarters + 2
    annuals. New files: `orcl_historical_quarterly_full.csv` (+ `_full_provenance.csv`),
    `orcl_fy2025_q4_derivation_support.csv`, `orcl_historical_full_checks.csv`,
    `templates/orcl_historical_quarterly_template_v2.csv` (125-row, regenerated
    from the 137-field dictionary; Gate 4's 120-row original left untouched).
  - **107 total reconciliation checks (pilot + full): 103 pass / 0 fail / 4 blocked**
    (each blocked item has a documented reason and follow-up, no hidden failures).
    CHECK_050 sum-of-quarters now closes for both fiscal years.
  - **D-016:** found two disclosure-evolution gaps distinct from Q-18 — no lease
    supplemental footnote exists in FY2025 Q1–Q3 10-Qs (BS_060/DEBT_050/DEBT_060
    genuinely not disclosed those quarters); FY2025 exact-millions IaaS/SaaS
    (REV_120/130) sourced from later FY26 releases' recast comparatives
    (precision upgrade over each period's own headline-only disclosure).
  - **D-017:** established the full-extraction file pair as the Gate 6+ input;
    Gate 5A pilot files retained unmodified as the audit trail.
  - C-01/C-02 quarterly series now fully closed and tied to their annual anchors
    for both fiscal years; C-06 quarterly series confirmed as a routine disclosure.
  - Deliverables: `GATE_5B_REVIEW.md`, `GATE_5B_EXTRACTION_LOG.md`.

## Work in progress

None mid-flight. Clean stopping point.

## Known issues / blockers

1. D-014 EBITDA definition awaits user ratification (PROF_160 labeled provisional).
2. All 8 earnings-call transcripts missing (Q-04); analyst-day deck missing (Q-05).
3. User thesis template blank (Q-06) — blocks Gate 8.
4. Preferred conversion terms need Certificate of Designations/prospectus (Q-11).
5. **SRC-016 capture defect** (clipped wide tables in the Q4 FY26 release PDF) —
   cosmetic; did not block any value across Gate 5A/5B. Re-capture still optional.
6. Blocked check items (documented, non-blocking for Gate 6): BS_070 non-current
   deferred-revenue split; CF_040 acquisitions caption mismatch (both years);
   CAP_020/commercial-paper Q4 FY26 split; FY2025 quarterly debt roll-forward.
7. Disclosure-matrix curated subset (63 fields) does not track BS_060/DEBT_050/
   DEBT_060 — the D-016 finding lives in the data dictionary notes instead.

## Next recommended action

Run Gate 6 historical reconciliation using the exact prompt in
`00_project_control/GATE_5B_REVIEW.md` §11.

## Restart note

If this file and the architecture docs disagree, the architecture docs govern
structure; this file governs sequencing/status. For historical values, use
`orcl_historical_quarterly_full.csv` / `_full_provenance.csv` — the Gate 5A pilot
files are the audit record of that session, not the current source of truth.
