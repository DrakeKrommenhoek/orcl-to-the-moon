# Gate 5B Extraction Log — Full Historical Extraction (FY2025 Q1 – FY2026 Q4)

Date: 2026-07-20 · Scope: extends the Gate 5A pilot (FY2026 Q1 + FY2026 Q4) to all
eight quarters plus both fiscal-year annual anchors. Companion files:
`orcl_historical_quarterly_full.csv` (template-shaped, 125 rows),
`orcl_historical_quarterly_full_provenance.csv` (per-value provenance, one row per
populated or not-disclosed cell), `orcl_fy2025_q4_derivation_support.csv`,
`orcl_fy2026_q4_derivation_support.csv` (from Gate 5A, unchanged),
`../reconciliations/orcl_historical_full_checks.csv`. The Gate 5A pilot files remain
in place unmodified as the audit record of that session; the full file supersedes
them for modeling purposes.

## 1. Sources opened (new to this session)

| SRC | File | Role |
|---|---|---|
| SRC-003 | ORCL_FY2025_Q1_10-Q_2024-08-31.pdf | Controlling, FY25 Q1 GAAP |
| SRC-004 | ORCL_FY2025_Q2_10-Q_2024-11-30.pdf | Controlling, FY25 Q2 GAAP |
| SRC-005 | ORCL_FY2025_Q3_10-Q_2025-02-28.pdf | Controlling, FY25 Q3 GAAP; nine-month base for FY25 Q4 |
| SRC-002 | ORCL_2025_10-K_FY_Ended_2025-05-31.pdf | Controlling, FY25 annual + year-end balance sheet |
| SRC-009 | ORCL_FY2025_Q1_Earnings_Release_2024-09-09.pdf | FY25 Q1 non-GAAP, KPIs |
| SRC-010 | ORCL_FY2025_Q2_Earnings_Release_2024-12-09.pdf | FY25 Q2 non-GAAP, KPIs |
| SRC-011 | ORCL_FY2025_Q3_Earnings_Release_2025-03-10.pdf | FY25 Q3 non-GAAP, KPIs |
| SRC-012 | ORCL_FY2025_Q4_Earnings_Release_2025-06-11.pdf | FY25 Q4 directly-reported statements, non-GAAP |
| SRC-007 | ORCL_FY2026_Q2_10-Q_2025-11-30.pdf | Controlling, FY26 Q2 GAAP |
| SRC-014 | ORCL_FY2026_Q2_Earnings_Release_2025-12-10.pdf | FY26 Q2 non-GAAP, KPIs |
| SRC-008 | ORCL_FY2026_Q3_10-Q_2026-02-28.pdf | Controlling, FY26 Q3 GAAP (already opened in Gate 5A for the Q4 derivation) |
| SRC-015 | ORCL_FY2026_Q3_Earnings_Release_2026-03-10.pdf | FY26 Q3 non-GAAP, KPIs |
| SRC-006, SRC-013, SRC-016, SRC-017, SRC-024 | (Gate 5A pilot sources) | Reused unchanged for FY26 Q1/Q4/annual |

## 2. Key structural finding: pre-FY26 disclosure gaps (D-016)

Comparing the FY25 Q1–Q3 10-Qs against the FY26 Q1 10-Q (already flagged for
captions under Q-18/D-013) surfaced a **second, independent disclosure-architecture
change** that Gate 4/5A had not anticipated:

- **No dedicated lease supplemental-balance-sheet footnote exists in the FY25 Q1–Q3
  10-Qs.** Operating lease ROU assets and the current/non-current lease-liability
  split are not disclosed anywhere in those filings (only embedded, undisaggregated,
  inside "Other non-current assets"/"Other non-current liabilities"). The dedicated
  lease note (with the ROU-asset/liability supplemental table now familiar from
  FY26 10-Qs) **first appears in the FY2025 10-K** (annual only) and becomes a
  standard 10-Q footnote starting FY26 Q1.
- Consequence: **BS_060, DEBT_050, DEBT_060 are genuinely not disclosed for FY2025
  Q1, Q2, and Q3** — not an extraction gap. They become available starting FY2025
  Q4/annual (10-K) and every quarter from FY2026 Q1 onward.
- The "revenues by offerings" footnote with exact-millions IaaS/SaaS dollars (used
  for REV_120/REV_130 from FY26 Q1 onward) also does not exist in the FY25 10-Qs;
  FY25 quarters only ever disclosed IaaS/SaaS at whole-billion headline precision in
  their *own* period's release (see §3).
- Recorded as **D-016** in `decision_log.md`.

## 3. Precision upgrade: FY25 IaaS/SaaS from later Oracle releases (also D-016)

The FY26 Q1 earnings release (SRC-013) and the FY26 Q4 release (SRC-016) both
publish a "CLOUD REVENUES BY OFFERINGS" supplemental table with **exact-millions**
quarterly comparatives for the full FY2025 fiscal year (Cloud applications /
Cloud infrastructure, Q1–Q4 and total). This is more precise than what each FY25
quarter's own release disclosed at the time (whole-billion headline bullets, e.g.
"$2.2 billion"). Because this is still an official Oracle release (rung 3, same as
the period's own release) — just published later as a comparative — it was adopted
as the primary value for REV_120/REV_130 across all FY25 quarters and the FY25
annual total, with the precision upgrade and its provenance explicitly noted in
every affected row. The original headline-billion disclosures are retained in the
`notes` column for cross-reference. This does not apply to any GAAP financial-
statement line — only to the supplemental (Layer 2) IaaS/SaaS dollar breakout.

## 4. Population counts (this session's additions)

Combined with the retained Gate 5A pilot values, the full provenance file now
carries **839 populated values** (475 reported, 256 calculated, 108 supplemental)
across FY2025 Q1–Q4, FY2026 Q1–Q4, and both annual anchors, plus **96 explicit
not-disclosed determinations**. Per-quarter value counts range from 87 (FY25 Q2/Q3,
reflecting the D-016 lease-footnote gap) to 95 (FY25 Q4, FY26 Q1, FY26 Q4).

## 5. Calculated fields

FY2025 Q2/Q3 standalone quarters use YTD differencing (Q2 = 6mo YTD − Q1; Q3 = 9mo
YTD − 6mo YTD) exactly as specified in `HISTORICAL_RECONCILIATION_PLAN.md` §15.
FY2025 Q4 = FY(10-K) − 9M(Q3 10-Q), with the FY25 Q4 release's directly-reported
standalone values used as the controlling figure and the derivation as validation
— same precedence rule as the Gate 5A FY26 Q4 pattern (D-015). All 37 FY25 Q4
derivations are in `orcl_fy2025_q4_derivation_support.csv`. FY2026 Q2/Q3 follow the
same YTD-differencing pattern as FY25 Q2/Q3, extended to the D-013 dual-presentation
captions (REV_011/REV_021/REV_147/COGS_011).

## 6. New conflicts/caption drift found during Q2/Q3 extraction

- **FY26 Q1 → Q2 cash-flow caption drift:** Q1 FY26 10-Q shows a standalone
  "Repayments of commercial paper, net" line; from Q2 FY26 onward this becomes
  "Proceeds from (repayments of) commercial paper **and other short-term
  financing**, net" — a combined caption. CF_050/CF_060 (senior notes/term-loan
  issuance and repayment) were kept on a consistent definition throughout and are
  unaffected; the commercial-paper/short-term-financing sub-line was not derived
  standalone per quarter to avoid mixing inconsistent captions (same discipline as
  the Gate 5A CAP_020/Q4 refusal, D-015 rule 8 in `EXTRACTION_PRECEDENCE_RULES.md`).
- **Mandatory convertible preferred stock issuance timing confirmed at the
  quarterly level:** DEBT_100 first appears at FY26 Q3 ($4,954M, issued 2026-02-05);
  CF_070 Q3 FY26 standalone equity issuance (4,963) is almost entirely the preferred
  raise; preferred dividends (DEBT_110) first appear at FY26 Q3 ($22M) — all
  internally consistent with the C-01/Q-11 findings from Gate 5A.
- **FY2025 quarterly debt roll-forward left BLOCKED** (CHK25Q4-09): reconstructing
  it quarter-by-quarter was outside this session's required-field scope; flagged as
  an optional Gate 6 follow-up if a trend view of C-01 is later wanted.

## 7. Rounding issues (consistent with the Gate 5A pattern)

The same ±$1M recast-rounding behavior observed in Gate 5A between a period's direct
release value and its FY-minus-prior-period derivation recurs throughout FY25 Q4
(COGS_030, OPEX_050, PROF_060, PROF_070, PROF_080 all differ by exactly $1M) and in
isolated FY25/FY26 Q2 lines (OPEX_070 standalone SBC, PROF_150 amortization
component). Convention unchanged: the more direct/granular disclosure controls; the
derivation is the validation check, not the stored value, except where no direct
disclosure exists (in which case the derived value is stored and labeled
`calculated`).

## 8. Extraction limitations carried forward or newly found

1. D-016 lease-footnote and IaaS/SaaS-precision gaps (§2–3) — genuine disclosure
   limitations of the FY25 10-Qs, not extraction misses.
2. CAP_010/CAP_020/CAP_030 (prepayments, short-term capex financing, net cash
   capex) remain not-disclosed for essentially all of FY25 — these are FY26
   phenomena per the FY26 10-K's own language ("no such prepayments... during
   fiscal 2025 and 2024").
3. KPI_030/040/060 (utilization, region counts, BYOH) remain blocked pending
   transcripts (Q-04) for both fiscal years.
4. FY2025 CF_040 (acquisitions) not populated as a distinct field this session
   (immaterial/nil in the periods examined; not required to complete the checks
   battery) — left `not_disclosed` for consistency rather than guessed at zero.
5. The Gate 5A SRC-016 capture defect (clipped wide tables) is unchanged; not
   revisited this session since it did not block any FY25/FY26 Q2-Q3 field.

## 9. Questions requiring human judgment

Unchanged from Gate 5A (D-014 EBITDA sign-off, C-01 gross-debt convention,
uncommenced-lease treatment) plus:

6. Whether the FY25 quarterly debt roll-forward (CHK25Q4-09, blocked) is worth
   building before Gate 6, or can stay deferred until it is actually needed.
7. Whether to correct the FY2025 Q1–Q3 disclosure-matrix entries for
   BS_060/DEBT_050/DEBT_060 from "TBD" to a confirmed "not disclosed pre-FY26"
   status (recommended; see architecture-change note in the Gate 5B review).
