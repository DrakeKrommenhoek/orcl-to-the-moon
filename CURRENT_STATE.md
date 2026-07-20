# CURRENT_STATE

Last updated: 2026-07-20 (Gate 5A pilot session)
Branch: `claude/oracle-historical-extraction-pilot-r6o3ov` (reset onto prior tip
`e06f7ae` of `claude/oracle-equity-model-mhmjq4`; remote = DrakeKrommenhoek/orcl-to-the-moon)

## Current phase

**Gate 5A (extraction pilot) COMPLETE.** Gates 1–4 completed earlier on 2026-07-20.
The two-quarter pilot (FY2026 Q1 + FY2026 Q4) validated the architecture, source
mapping, both extraction methods (direct and FY-minus-9M), provenance capture, and
the checks battery. **Next: Gate 5B full extraction (FY2025 Q1 – FY2026 Q3).**

## Completed work

- Gates 1–3: inventory, manifest (24 sources), duplicate review, conflict register.
- Gate 4: three-layer architecture, data dictionary, mapping, matrix, template,
  reconciliation plan, precedence rules.
- Branch-sync: FY2026 10-K registered as SRC-024.
- **Gate 5A (this session):**
  - Extracted 249 fully-provenanced values (95 FY26 Q1, 95 FY26 Q4, 59 FY26 annual);
    28 explicit not-disclosed determinations; 44-row Q4 derivation support file.
  - 37 reconciliation checks: 34 pass / 0 fail / 3 blocked-with-reason.
  - **Resolved: Q-18** (true FY26 filed-statement reclassification; dual-presentation
    fields added per D-013), **C-01** (gross debt = $129,541M borrowings-only; $135B
    secondary claim included the $4,954M preferred), **C-02** (FY26 depreciation =
    $7,623M, depreciation-only), **C-06** ($260B uncommenced leases, off balance
    sheet, future-commitment treatment).
  - **Q-10:** EBITDA recommendation issued (D-014, provisional): GAAP operating
    income + CF depreciation + amortization of intangibles; awaiting user sign-off.
  - Architecture: dictionary/mapping now 137 fields (added REV_011, REV_021, REV_147,
    COGS_011, OPEX_065); Layer 3 bridge amended for FY26 presentation; D-015 fixes
    Q4 precedence (direct release value controls; FY−9M validates; caption-mismatch
    derivations refused).
  - Deliverables: `GATE_5A_PILOT_REVIEW.md`, `EBITDA_DEFINITION_MEMO.md`,
    `PILOT_EXTRACTION_LOG.md`, pilot/provenance/derivation/checks CSVs.

## Work in progress

None mid-flight. Clean stopping point.

## Known issues / blockers

1. **SRC-016 capture defect:** FY26 quarterly columns of the Q4 release supplemental
   tables are clipped out of the PDF capture — Q4 IaaS/SaaS exact millions were
   derived (FY−9M) instead. Re-capture recommended before/during Gate 5B (user).
2. D-014 EBITDA definition awaits user ratification (PROF_160 labeled provisional).
3. All 8 earnings-call transcripts missing (Q-04); analyst-day deck missing (Q-05).
4. User thesis template blank (Q-06) — blocks Gate 8.
5. Preferred conversion terms need Certificate of Designations/prospectus (Q-11).
6. Blocked check items for 5B follow-up: BS_070 non-current deferred revenue split;
   CF_040 acquisitions caption mismatch; CAP_020/CP Q4 split (see checks CSV).
7. Template regeneration from the 137-field dictionary deferred to Gate 5B start
   (Gate 4 original intentionally untouched).

## Next recommended action

Run Gate 5B full extraction (FY2025 Q1 – FY2026 Q3) using the exact prompt in
`00_project_control/GATE_5A_PILOT_REVIEW.md` §18.

## Restart note

If this file and the architecture docs disagree, the architecture docs govern
structure; this file governs sequencing/status. The pilot two-file pattern
(values + provenance) is the Gate 5B standard (D-015).
