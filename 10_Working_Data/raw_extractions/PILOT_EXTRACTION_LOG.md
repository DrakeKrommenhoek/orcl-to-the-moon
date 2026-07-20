# Gate 5A Pilot Extraction Log

Date: 2026-07-20 · Scope: FY2026 Q1 (ended 2025-08-31) and FY2026 Q4 (ended
2026-05-31) only, plus FY2026 annual anchors. Extractor: Claude Code session
(Gate 5A). Companion files: `orcl_historical_quarterly_pilot.csv` (template-shaped),
`orcl_historical_quarterly_pilot_provenance.csv` (per-value provenance),
`orcl_fy2026_q4_derivation_support.csv`,
`../reconciliations/orcl_historical_pilot_checks.csv`.

## 1. Sources opened (all read as full-text extractions of the repo PDFs)

| SRC | File | Role in pilot |
|---|---|---|
| SRC-006 | ORCL_FY2026_Q1_10-Q_2025-08-31.pdf | Controlling source, Q1 GAAP statements + footnotes |
| SRC-013 | ORCL_FY2026_Q1_Earnings_Release_2025-09-09.pdf | Q1 non-GAAP, supplemental revenue tables, KPIs, TTM FCF |
| SRC-024 | ORCL_2026_10-K_FY_Ended_2026-05-31.pdf | Controlling source, FY26 annual + year-end balance sheet; C-01/C-02/C-06 |
| SRC-008 | ORCL_FY2026_Q3_10-Q_2026-02-28.pdf | Nine-month cumulative values for Q4 = FY − 9M only |
| SRC-016 | ORCL_FY2026_Q4_Earnings_Release_2026-06-10.pdf | Directly reported standalone Q4 statements, non-GAAP, RPO |
| SRC-017 | ORCL_FY2026_Q4_Earnings_Slides.pdf | Q4 KPIs (utilization, GW, Fusion/NetSuite, net cash capex) |
| SRC-002 / SRC-003 | FY25 10-K / FY25 Q1 10-Q | Caption comparison only (Q-18); no values extracted |

## 2. Tables and notes used

- SRC-006: statements of operations (PDF p.7), balance sheets (p.5), cash flows
  (p.10), Note 1 basis-of-presentation reclass language (p.11), RPO footnote (p.11),
  non-operating/interest income note (p.15), leases note incl. uncommenced
  commitments (p.21), software/cloud revenues by offerings (p.30/32), EPS note (p.32).
- SRC-013: headline bullets (p.1), GAAP statements (p.3-4), non-GAAP reconciliation
  incl. SBC by category (p.4-5), balance sheet (p.6), cash flows (p.7), TTM FCF (p.8),
  supplemental analysis of GAAP revenues (p.9-10), Appendix A (OBBBA $958M).
- SRC-024: statements of operations (p.67), comprehensive income (p.68), balance
  sheets (p.66), cash flows (p.70), Note 1 (RPO p.74, prepayments p.75,
  concentrations p.77), non-operating note (p.81), Note 4 PP&E (p.83), Note 6 debt
  (p.85-86), Note 9 leases/commitments (p.90-92), revenue disaggregation by
  offerings (p.104), MD&A liquidity/equity items (p.55).
- SRC-008: statements of operations, three and nine months (p.6), cash flows nine
  months (p.9), interest income note (p.14), revenues by offerings (p.33).
- SRC-016: Q4 statements (p.5), Q4 non-GAAP reconciliation (p.6-7), FY statements
  (p.8), FY non-GAAP (p.9-10), balance sheet (p.10-11), cash flows (p.11-12), TTM
  FCF (p.12-13), net cash outlay for capex (p.13), headline/RPO/capital-program text
  (p.1-3).
- SRC-017: highlights (p.4-5), cloud revenue detail (p.6), infrastructure highlights
  (p.8), long-term outlook (p.15), FY27/Q1-FY27 guidance (p.16-17).

## 3. Population counts

- Values recorded with full provenance: **249** (95 FY2026_Q1, 95 FY2026_Q4,
  59 FY2026_annual).
- Classification mix: 141 reported · 66 calculated · 42 supplemental.
- Explicit not-disclosed determinations: **28** (each with a reason row in the
  provenance file).
- All FY2025 Q1–Q4, FY2026 Q2–Q3 and FY2025_annual cells: **blank by scope** (Q3
  9M inputs live only in the derivation support file, as instructed).

## 4. Fields left blank / marked not disclosed (highlights)

- REV_010 / REV_020 / COGS_010 / REV_140 (FY26): filed captions discontinued by the
  FY26 presentation change (Q-18); successors REV_011/REV_021/COGS_011 + REV_147.
- OPEX_050 / OPEX_060 (Q4): 10-K and Q4 release disclose only combined
  "Restructuring and other" (new OPEX_065 = 823); 9M splits exist (55 / 961).
- CF_040 acquisitions (Q1 and Q4): FY26 CF presentation has no separate
  acquisitions caption; FY caption includes acquisitions inside the securities-purchases
  line while 9M caption does not → derivation refused (caption-consistency rule).
- CAP_020 Q4 / commercial paper Q4: 9M combines CP + short-term capex financing in
  one line; FY splits them → only a combined Q4 figure (−1,219) derivable (DRV-40).
- CAP_030 (net cash capex): disclosed only on trailing-4Q/FY basis ($48B FY26);
  quarterly standalone not disclosed.
- BS_070: 10-Q/10-K balance-sheet face shows current deferred revenues only;
  non-current portion not separately disclosed → current-only value carried, flagged.
- KPI_030/040 (Q1), KPI_060/070 (Q1), CAP_010 (Q1): no disclosure in Q1 materials.
- DEBT_090: no single weighted-average rate disclosed (per-instrument only).

## 5. Calculated fields

All Q4 = FY − 9M derivations are enumerated in
`orcl_fy2026_q4_derivation_support.csv` (44 rows, DRV-01 … DRV-44) with both
source citations, formula, result, direct-Q4 validation value where one exists, and
the rounding difference. Other calculated fields (bridges, margins, FCF, gross/net
debt, cRPO, EBITDA) carry their formula in the provenance file.

## 6. Conflicts found / resolved this session

- **C-01 resolved** — FY26 gross borrowings = 7,199 + 122,342 = **$129,541M**,
  matching Note 6 carrying total. The $135B secondary claim ≈ borrowings + $4,954M
  preferred (= $134.5B) — a definitional difference, not a different date.
- **C-02 resolved** — FY26 depreciation = **$7,623M** (CF statement; Note 4 "$7.6B").
  The ~$4.8B Research Pack series is an unsupported estimate.
- **C-06 resolved** — **$260B** uncommenced lease commitments at 5/31/26 (Note 9);
  commence Q1 FY27–FY29, 15–19-year terms; excluded from balance-sheet lease
  liabilities; includes a $3.3B lessor-borrowing guarantee maturing Sep 2026.
- New finding (no conflict number needed): the ±$1M recast-rounding differences
  between Q4 release direct values and FY−9M derivations on five expense/below-op
  lines (documented in checks CHK-Q4-02/04, all within tolerance).

## 7. Rounding issues

- Five Q4 lines differ by exactly $1M between direct release values and FY−9M
  derivations (COGS_020, OPEX_020, OPEX_040, OPEX_065, PROF_050 — and pretax/tax by
  the same $1M). Cause: Oracle's recast of prior captions rounds independently.
  Convention adopted: **direct release value controls; derivation is validation.**
- Q4 IaaS/SaaS at headline precision ($5.8B/$4.1B) vs derived exact ($5,787/$4,126):
  derived exact values adopted (both round correctly to the headline).
- RPO release rounding (455 vs footnote 455.3): footnote controls.

## 8. Extraction limitations

1. **SRC-016 capture defect:** the print-to-PDF of the Q4 release clips the right
   edge of wide tables — the FY2026 quarterly columns of the supplemental revenue
   analysis, TTM FCF (Q3/Q4 FY26 columns), and net-cash-outlay tables are missing
   from the repo capture. Exact-millions Q4 IaaS/SaaS therefore had to be derived
   (FY − 9M) rather than read directly. Recommend re-capturing the release (or
   pulling the 8-K exhibit) before Gate 5B. SRC-013 has the same defect on the
   prior-year columns of its non-GAAP table (current-year columns intact).
2. No Q4 10-Q exists (normal); Q4 balance-sheet values are 10-K year-end balances.
3. Transcripts (Q-04) and analyst-day deck (Q-05) still missing — KPI_030 Q1,
   utilization/BYOH commentary beyond slides not extractable.
4. Preferred-stock terms (conversion mechanics) require the Certificate of
   Designations/prospectus — not in repo (Q-11 unchanged).
5. FY26 10-K income statement merges "Acquisition related and other" into
   "Restructuring and other"; FY26 annual OPEX_050/OPEX_060 individually are
   therefore not disclosed (only 9M splits are).

## 9. Questions requiring human judgment

1. Ratify the EBITDA recommendation (D-014 / Q-10) — see
   `11_Analysis/historical/EBITDA_DEFINITION_MEMO.md`.
2. Confirm the C-01 gross-debt convention: borrowings-only ($129,541M), with
   preferred, finance leases ($7,701M) and operating leases ($30,190M) carried as
   separate EV-bridge components (interacts with Q-11/Q-13).
3. Approve treating uncommenced leases ($260B) as a scheduled future commitment
   (capacity/committed-capital analysis), not current debt.
4. Decide whether to re-provide a complete Q4 release capture (recommended) or
   accept derivation-based Q4 sub-streams.
5. Approve scaling to Gate 5B (all eight quarters) with the amended architecture.
