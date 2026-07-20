# Gate 5A Review — Historical Extraction Pilot

Date: 2026-07-20 · Session scope: FY2026 Q1 and FY2026 Q4 only (two-quarter pilot).
Branch: `claude/oracle-historical-extraction-pilot-r6o3ov` (reset onto the prior
working branch tip `e06f7ae`, which contained all Gate 1–4 work + SRC-024).

## 1. Pilot scope

Prove the Gate 4 architecture end-to-end on two structurally different quarters:
FY2026 Q1 (direct 10-Q/release extraction; Q1 YTD = standalone) and FY2026 Q4
(no 10-Q; direct release statements + FY-minus-nine-month derivations anchored on the
filed 10-K). FY2026 annual anchors extracted where they drive Q4 or resolve conflicts.
No other quarter populated; no forecasting, comps, valuation, or Excel work.

## 2. Sources used

SRC-006 (Q1 10-Q, controlling for Q1 GAAP), SRC-013 (Q1 release), SRC-024 (FY26 10-K,
controlling for FY/annual + year-end balance sheet), SRC-008 (Q3 10-Q, nine-month
inputs only — recorded solely in the derivation support file), SRC-016 (Q4 release),
SRC-017 (Q4 slides). SRC-002/SRC-003 opened for caption comparison only (Q-18).
AI research reports (SRC-019/020): **not used for any value** (verified
programmatically).

## 3–7. Population statistics

| Metric | Count |
|---|---|
| FY2026 Q1 values populated (with full provenance) | **95** |
| FY2026 Q4 values populated | **95** |
| FY2026 annual anchor values | 59 |
| Total provenance rows (values) | 249 |
| Directly reported | 141 |
| Calculated (each with formula) | 66 |
| Supplemental disclosures | 42 |
| Explicit not-disclosed determinations | 28 |
| Q4 derivation rows documented | 44 (2 refused for caption inconsistency) |

## 8. Reconciliation checks

**37 checks: 34 PASS · 0 FAIL · 3 BLOCKED** (`10_Working_Data/reconciliations/
orcl_historical_pilot_checks.csv`). No failures. Blocked items (with follow-ups):
BS_070 non-current deferred revenue not separately disclosed; CF_040 acquisitions
derivation refused (FY/9M caption mismatch); CAP_020/commercial-paper Q4 split not
derivable (9M combines lines). Notable passes: all five Q4 revenue captions tie
FY−9M vs. direct at diff 0; non-GAAP bridges exact both quarters; EPS ties within
$0.01 including the new preferred-dividend mechanics; FY26 cash tie and Q4 cash tie
exact; FY debt roll-forward residual $107M explained (non-cash discount/issuance-cost
amortization) within documented tolerance.

## 9. C-01 — RESOLVED

FY26 gross debt (DEBT_030) = **$129,541M** (7,199 current + 122,342 non-current;
equals Note 6 carrying total; gross principal $130,105M). The $135B secondary figure
≈ borrowings + $4,954M mandatory convertible preferred (definitional inclusion, not a
different date). Convention: gross debt = borrowings only; preferred, finance leases
($7,701M), operating leases ($30,190M) tracked separately. Details in
`source_conflicts.md`.

## 10. C-02 — RESOLVED

FY26 depreciation = **$7,623M** (depreciation only, CF statement; Note 4 "$7.6B").
Framework correct; Research Pack ~$4.8B series unsupported. Quarterly tie verified to
the derivable extent (Q1 1,351 + mid 3,857 + Q4 2,415 = 7,623).

## 11. C-06 — RESOLVED

**$260B** uncommenced lease commitments as of 2026-05-31 (Note 9): data centers,
commencing Q1 FY27–FY29, 15–19-year terms, **not** on the balance sheet; includes a
$3.3B lessor-borrowing guarantee. Modeled as future commitment (DEBT_070), not
current debt. Quarterly series available from 10-Qs (Q1: $99.8B).

## 12. Q-10 — recommendation issued (D-014, provisional)

Primary EBITDA = GAAP operating income + CF depreciation + amortization of
intangibles (FY26: $29,900M). SBC not added back; restructuring in; gains excluded by
construction. Memo: `11_Analysis/historical/EBITDA_DEFINITION_MEMO.md`. Awaiting
user sign-off; PROF_160 populated and labeled provisional.

## 13. Q-18 — RESOLVED

True filed-statement reclassification effective FY26 Q1 (Cloud/Software captions,
comparatives recast, exact ties), plus an expense-line relabel, a 10-K-level
"Restructuring and other" merge, and new preferred-dividend/NIAC EPS mechanics.
Full evidence in `open_questions.md` Q-18 entry. Handled via dual-presentation
Layer 1 (D-013) — no forced renaming; bridge documented.

## 14. Architecture changes made (D-013, D-015)

1. Five fields added: REV_011, REV_021, REV_147, COGS_011, OPEX_065 (dictionary and
   mapping now 137 rows, still 1:1; stable IDs preserved; nothing redefined).
2. Layer 3 bridge amended for FY26 presentation: REV_330 = REV_145 (directly
   disclosed — better than the residual formula), REV_340 = REV_147.
3. Two-file extraction pattern: template-shaped values file + long-format provenance
   file (per-value source/section/classification/formula/precision).
4. Q4 precedence rule: direct release value controls; FY−9M is validation;
   derivations refused on caption mismatch.

## 15. Source-mapping / matrix changes recommended (and made)

- Stale "SRC-024 NOT YET RECEIVED" annotations cleared from the mapping.
- Disclosure-matrix corrections noted: REV_120/130 now exact-$M in 10-Q footnotes
  (rung 2); DEBT_070 and RPO_050 are quarterly disclosures in FY26, not annual-only.
- Manifest: capture-defect notes added to SRC-013/SRC-016 (clipped right-edge tables);
  **recommend re-capturing the Q4 release (or its 8-K exhibit) before Gate 5B.**

## 16. Is the template ready to scale?

Structurally yes, with the D-013 field additions. The Gate 4 template file itself was
left untouched (structural-validation requirement); regenerate it from the 137-row
dictionary at the start of Gate 5B so new quarters inherit the dual-presentation rows.

## 17. Should Gate 5B begin?

**Yes.** The pilot validated: source mapping, both extraction methods (direct and
FY−9M), provenance capture, blank-beats-guess handling, caption-change handling, and
the checks battery — 0 failed checks, 0 structural-validation errors. Known
imperfections (clipped SRC-016 tables, missing transcripts) do not block FY25 Q1 –
FY26 Q3 extraction.

## 18. Exact next prompt (Gate 5B)

> Continue the Oracle equity-research project. This session is Gate 5B: full
> historical extraction. Read CLAUDE.md, CURRENT_STATE.md, all of 00_project_control/
> (especially GATE_5A_PILOT_REVIEW.md, decision_log D-013/D-014/D-015, and the
> resolved C-01/C-02/C-06 and Q-18 entries), the architecture docs, and the Gate 5A
> pilot files in 10_Working_Data/raw_extractions/. First regenerate the extraction
> template from the 137-field dictionary (preserving the Gate 4 original), then extend
> the pilot files (same two-file pattern: values + provenance) to cover FY2025 Q1 –
> FY2026 Q3, using SRC-003/004/005 (FY25 10-Qs), SRC-009/010/011/012 (FY25 releases),
> SRC-002 (FY25 10-K, controlling for FY25 annual + FY25 Q4 = FY − 9M), and
> SRC-006/007/008 + SRC-013/014/015 for FY26 Q1–Q3. FY25 quarters use the pre-FY26
> captions (REV_010/020, COGS_010); FY26 quarters use D-013 presentation-B fields.
> Record every FY25-Q4-style derivation in a derivation support file; run the full
> checks battery including CHECK_050 sum-of-quarters ties for FY25 and FY26 and the
> quarterly debt roll-forward; do not populate Layer 3 except via the documented
> bridges; blank beats guess (D-011). Do not start Gate 6 cross-source reconciliation
> beyond the intra-document and derivation checks, and do not begin forecasting or
> the Excel model. Update project-control files and commit on the designated branch.

Optional user actions that improve 5B: re-capture SRC-016 complete tables; provide
earnings-call transcripts (Q-04) and the analyst-day deck (Q-05); ratify D-014.
