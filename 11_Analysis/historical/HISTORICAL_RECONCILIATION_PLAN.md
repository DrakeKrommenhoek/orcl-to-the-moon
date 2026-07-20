# Historical Reconciliation Plan (Gate 6 specification)

Written at Gate 4 (2026-07-20). This plan defines *how* Gate 6 will validate the data
extracted at Gate 5. **No figures are calculated here.** Every check below has a CHECK_
field in the data dictionary; a check that cannot run (missing input) is reported as
`blocked`, never silently skipped. All checks must pass — or carry a documented,
user-visible exception — before any figure is quoted or modeled.

## Tolerances

- Filed statement values: exact match (they are transcriptions, not calculations).
- Cross-document comparisons (release vs. 10-Q/10-K): within disclosed rounding
  (± $1M on millions-stated figures; ± $0.1B on billions-stated; ± $0.01 on EPS).
- Residual/bridge values: within accumulated rounding of inputs; the tolerance used is
  recorded next to each result.
- Any breach outside tolerance → entry in `source_conflicts.md` before further use.

## 1. Revenue category additivity (CHECK_010)

Per quarter: REV_010 + REV_020 + REV_030 + REV_040 = REV_050 exactly, from the same
document. Run separately per source (10-Q vs. release) before cross-source comparison.

## 2. Supplemental cloud metrics vs. reported categories (CHECK_030, CHECK_040)

- REV_120 + REV_130 = REV_110 within rounding, same release.
- REV_110 ≤ REV_010 (cloud cannot exceed cloud-services-and-license-support) under the
  pre-FY26 presentation; verify relationship still holds under any FY26 regrouping (Q-18).
- Residual support (REV_330 = REV_010 − REV_110) compared to MD&A license-support line
  (REV_145) where the split exists; divergence beyond rounding → conflict entry.

## 3. GAAP vs. non-GAAP operating income (CHECK_090)

Rebuild non-GAAP from GAAP + itemized reconciling adjustments (SBC, intangible
amortization, acquisition/restructuring, other) per the release table; must equal the
release's stated non-GAAP figure exactly. Same procedure for net income and EPS. Any
change in reconciling-item composition across quarters is logged (definition drift).

## 4. EBITDA and depreciation (CHECK_060 support; C-02)

- Quarterly standalone depreciation (PROF_140) via YTD differencing (§15 below).
- FY totals: sum of four standalone quarters = 10-K annual depreciation (FY25 vs.
  SRC-002; FY26 blocked until SRC-024). This is the designated resolution test for C-02.
- EBITDA is validated only after Q-10 fixes its definition; then EBITDA components must
  re-derive from validated PROF_010/140/150 inputs.

## 5. Capital expenditures

Same YTD differencing as OCF; FY25 annual tie to SRC-002; FY26 annual tie blocked until
SRC-024 (interim cross-check: FY26 Q4 release cash-flow presentation). Cross-check
against management commentary on gross vs. net cash capex (CAP_030) — but the *filed*
capex line is controlling (precedence rules §1).

## 6–8. Operating cash flow, free cash flow, cash

- OCF: YTD differencing; sum of standalone quarters = filed FY figure (CHECK_050/060).
- FCF: recompute CF_030 = CF_015 − CF_025; separately compare the *TTM* aggregation of
  CF_030 to Oracle's own TTM FCF table (CF_035) where published — divergence must be
  explained by definitional difference, and that difference documented once.
- Cash: balance-sheet cash movement (BS_010 t vs. t−1) = CF statement net change ±
  FX effect line (CHECK_100), quarterly (standalone) and annually.

## 9. Debt (CHECK_080; C-01)

- Gross debt roll-forward per quarter: opening DEBT_030 + issuance (CF_050) − repayments
  (CF_060) ± reclassifications/discount amortization ≈ closing DEBT_030; unexplained
  residual beyond tolerance → conflict entry.
- FY26 year-end DEBT_030 from the FY26 10-K balance sheet is the designated resolution
  of C-01. Record whether the $135B claim included the preferred or leases.

## 10. Interest expense

Quarterly income-statement values sum to FY total (CHECK_050). Sanity ratio: interest
expense vs. average gross debt (flag implausible implied rates for investigation, not
adjustment).

## 11–12. Share count and EPS (CHECK_070)

- PROF_100 / SHARE_020 reproduces PROF_120 within $0.01 (and non-GAAP analog). Where it
  doesn't (antidilution, rounding, preferred dividends in the numerator after FY26
  issuance), the cause is documented — this check is also the detector for whether
  preferred dividends have begun reducing income available to common (Q-11 input).
- Weighted-average share progression: quarter-over-quarter change flagged if > ±2%
  without a known driver (buyback, ATM, convertible).

## 13. RPO (C-07)

Footnote value (10-Q/10-K) is controlling; release/slide quotes must agree within
rounding. cRPO recomputed as RPO_010 × RPO_020 and labeled calculated. The eight-quarter
series is assembled *only* from primary documents; the AI-report series is compared
afterward as a diagnostic (differences noted in C-07, never adopted).

## 14. Annual totals (CHECK_050)

For every flow field: standalone Q1+Q2+Q3+Q4 = 10-K annual figure. FY2025 fully testable
now (SRC-002 + three 10-Qs + releases). FY2026 testable only for fields in the FY26 Q4
release, until SRC-024 arrives. Stock (balance) fields instead check Q4 period-end =
10-K balance sheet.

## 15. Standalone quarters from YTD 10-Q cash flows — formula and validation

10-Q cash-flow statements are cumulative (YTD). For any YTD-reported flow F:

```
F_Q1 = YTD_Q1
F_Q2 = YTD_Q2 − YTD_Q1
F_Q3 = YTD_Q3 − YTD_Q2
F_Q4 = FY_total − YTD_Q3        (FY from 10-K; interim: Q4 release CF presentation)
```

Validation battery (CHECK_060):
1. Re-summation: computed standalones re-sum to each filed YTD value and the FY total.
2. Cross-document: where a release presents quarterly or TTM cash-flow data, compare.
3. Sign/scale sanity: standalone values plausible vs. neighboring quarters; a derived
   negative on a normally positive line triggers review of the two YTD inputs first
   (transcription error is the most common cause).
4. Derived Q4 values are tagged `calculated` (per CLAUDE.md validation standards), and
   FY26 Q4 derivations remain `provisional` until SRC-024 replaces the release-based FY
   anchor with the filed one.
5. FX line: the "effect of exchange rate changes" line participates in the cash tie
   (CHECK_100) and is differenced like any other YTD line.

## Execution order at Gate 6

1. Intra-document checks (additivity, EPS ties) per quarter.
2. YTD differencing + re-summation.
3. Cross-document checks (release vs. filing).
4. Annual ties (FY25 now; FY26 when SRC-024 arrives).
5. Bridge/L3 checks (CHECK_020/030/040).
6. Conflict resolutions recorded in `source_conflicts.md` (C-01, C-02, C-07 candidates).
7. Checks dashboard appended to the extraction workbook/CSV with pass/fail/blocked per
   check per quarter.
