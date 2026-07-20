# Extraction Precedence Rules

Gate 4 · 2026-07-20. Binding for all Gate 5+ extraction. Complements the source-authority
hierarchy in `CLAUDE.md`; where they appear to differ, `CLAUDE.md` governs and the
difference is logged as an open question.

## Precedence ladder (highest wins)

1. **Filed SEC financial statement** (10-K/10-Q statements themselves)
2. **Filed footnote or supplemental table** in the same or a related SEC filing
3. **Oracle earnings release** (including its GAAP/non-GAAP reconciliation tables)
4. **Oracle earnings presentation (slides)**
5. **Oracle earnings-call transcript**
6. **Other official management presentation** (analyst day, IR deck)
7. **Reputable market-data or financial-press source**
8. **AI research report** (`01_Research_Outputs/`)
9. **Analyst assumption** (ours; always tagged `assumed`)

Rules of use:
- A lower rung may *supply* a value only when no higher rung discloses it, and the value
  is tagged with its actual source ID and classification.
- Rungs 8–9 may never supply **historical financial values**. Rung 8 is for hypotheses,
  cross-checks, and framework design only. Rung 7 may supply market data (prices,
  consensus) with explicit as-of dates — never Oracle accounting figures.
- Every extracted value cites: SRC-ID, section/table, period, and classification
  (`reported | guided | consensus | calculated | assumed`).

## Specific handling rules

1. **Filing amendments (10-K/A, 10-Q/A):** an amendment outranks the original for the
   amended items only; both stay in the manifest, the original is never deleted; the
   manifest note records what was amended.
2. **Restatements / reclassifications:** store both vintages ("as originally reported"
   and "as restated/reclassified"), each labeled with its filing of origin. The model
   uses the latest-filed vintage; trend analysis states which vintage it uses. Silent
   overwriting is prohibited.
3. **GAAP vs. non-GAAP:** separate fields, never mixed in one series. Non-GAAP values
   come only from Oracle's own reconciliation tables, stored with their reconciling
   items; we do not construct "our own non-GAAP" (an analyst-adjusted metric would be a
   new `calculated` field with a documented formula).
4. **Constant-currency vs. reported growth:** separate fields (e.g., REV_060 vs.
   REV_070). CC values are Oracle-computed, tagged as such, and never derived by us.
5. **Annual vs. quarterly figures:** quarterly fields never take annual values; annual
   anchors live in annual columns and drive Q4 derivation (FY − 9M) and CHECK_050 ties.
6. **YTD vs. standalone quarters:** 10-Q cash-flow (and any other YTD) figures are stored
   as YTD in the as-filed field; standalone values exist only in the designated
   calculated fields via the differencing formulas in `HISTORICAL_RECONCILIATION_PLAN.md`
   §15. Never enter a YTD value into a standalone field.
7. **Rounded management disclosures:** keep the precision as stated ("$18.1B" is not
   $18,100M). Store magnitude + stated precision; checks use rounding-aware tolerances.
   Release-level dollars (IaaS/SaaS) keep release precision and are not falsely
   millionized.
8. **Release vs. later filing conflict:** the filing wins (rung 1–2 over 3), but the
   conflict is first recorded in `source_conflicts.md` with both values, then resolved —
   per CLAUDE.md's "higher authority wins only after the conflict is documented."
9. **Historical estimates embedded in research reports:** unusable as data, full stop.
   They may motivate a hypothesis ("Oracle disclosed IaaS dollars in the Q2 release —
   verify") but the extracted value must come from rungs 1–6. The disclosure matrix
   marks such series `EST` = exists only as estimate = unusable. This implements C-03,
   C-04, C-08 and D-005.
10. **Same-rung disagreement** (e.g., two footnotes): prefer the more specific/detailed
    table; document the discrepancy in `source_conflicts.md` regardless of size.
11. **Transcripts (rung 5):** management numbers spoken on calls are usable only when
    not disclosed in 1–4, tagged `reported (oral)` with speaker and quarter, and flagged
    for replacement if a written source later provides the figure.
12. **Blank beats guess:** when no rung 1–6 source discloses a value, the cell stays
    blank with status `not_disclosed`. This is a feature of the dataset, not a defect.
