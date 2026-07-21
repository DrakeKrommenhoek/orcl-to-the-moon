# Gate 6 Review — Historical Reconciliation

Date: 2026-07-20 · Session scope: cross-document reconciliation of the Gate 5A/5B
extraction, following `HISTORICAL_RECONCILIATION_PLAN.md` §"Execution order at
Gate 6" steps 3–7 (steps 1–2 and most of step 4 were already executed during
extraction; this session completes the remaining cross-document, RPO, and
bridge-consolidation work and produces the dashboard). Branch:
`claude/oracle-historical-extraction-pilot-r6o3ov`.

## 1. What Gate 6 added beyond Gate 5A/5B

Gate 5A/5B already ran intra-document checks (additivity, EPS ties), YTD
differencing/re-summation, and annual ties (CHECK_050 closed for both fiscal
years). Gate 6 executed the remaining reconciliation-plan steps that require
**independently re-opening a second document** for the same fact rather than
trusting the single source used at extraction time:

1. **Cross-document GAAP statement checks (10-Q vs. release)** for all six
   quarters where both exist (FY2025 Q1–Q3, FY2026 Q1–Q3): every revenue,
   expense, operating-income, interest, non-operating, pretax, tax, net-income,
   EPS, and share-count line compared by direct text diff between the two
   independently-transcribed source captures.
2. **Cross-document balance-sheet checks** for the same six quarters, plus a
   confirmation that the FY2025/FY2026 Q4 release and 10-K balance sheets are
   identical (already used as the same source value during extraction; recorded
   as a Gate 6 check for completeness).
3. **RPO cross-document check (C-07 resolution)** — footnote vs. release headline
   for all eight quarters, plus recomputed cRPO.
4. **Bridge/L3 consolidation** — verified CHECK_020 (six-stream additivity) holds
   in every one of the eight quarters via a single programmatic pass over the
   full provenance file, consolidating what had been checked per-quarter during
   extraction into one dashboard-level result.

## 2. Results

**Zero discrepancies found.** Every 10-Q GAAP statement line matches its
same-quarter earnings release exactly, digit for digit, in all six quarters
checked. Every balance sheet ties. All eight RPO footnote values round exactly
to their release headline. The six-stream revenue bridge is additive with zero
residual in all eight quarters.

## 3. C-07 — RESOLVED

Full RPO_010 series cross-verified footnote-vs-release for FY2025 Q1 – FY2026 Q4
(footnote controlling, release validating): $99.1B / $97.3B / $130.2B / $137.8B /
$455.3B / $523.3B / $552.6B / $638.0B — 8/8 quarters tie. cRPO recomputed for
each quarter (FY25: $37.7B/$37.9B/$40.4B/$45.5B; FY26: $45.5B/$52.3B/$66.3B/
$76.6B), consistent with the Framework's ~10–12% current-RPO narrative but now
sourced from the filed percentage, not the estimate. The Research Pack's
FY24-inclusive 12-quarter series remains out of scope (FY24 extension not
authorized, Q-03) and unusable. Full detail in `source_conflicts.md`.

## 4. Consolidated checks dashboard

`10_Working_Data/reconciliations/orcl_gate6_consolidated_dashboard.csv` merges
all three check files (Gate 5A pilot, Gate 5B full, Gate 6 cross-document) into
one 140-row index with a `source_session` column identifying provenance.

| Session | Checks | Pass | Blocked | Fail |
|---|---|---|---|---|
| Gate 5A pilot | 37 | 34 | 3 | 0 |
| Gate 5B full | 70 | 69 | 1 | 0 |
| Gate 6 cross-document | 33 | 33 | 0 | 0 |
| **Total** | **140** | **136** | **4** | **0** |

The four blocked items are unchanged from Gate 5B (BS_070 non-current
deferred-revenue split; CF_040 acquisitions caption mismatch; CAP_020/
commercial-paper Q4 FY26 split; FY2025 quarterly debt roll-forward) — each has a
documented reason and is a scope decision, not a data gap. **Zero failures across
all 140 checks run over three sessions.**

## 5. Conflict register status after Gate 6

C-01, C-02, C-06, C-07 all **RESOLVED**. C-03/C-04/C-08 resolved by treatment
(AI-report figures excluded, per D-005/D-011). C-05 (financing-plan
cross-reference), C-09/C-10 (comps), C-11 (guidance vs. consensus) remain open —
all are Gate 9+ scope (comparable companies, valuation), not historical-extraction
scope, and were never assigned to Gate 5/6 in the Gate 4 architecture.

## 6. Is the historical dataset ready for Gate 7 (forecast-driver design)?

Yes. All required historical fields for FY2025–FY2026 are extracted, provenanced,
intra-document-checked, YTD-differenced and re-summed, annually tied, and now
cross-document-verified against a second independent source with zero
discrepancies. The four blocked items are all non-required-field edge cases that
do not block forecast-driver design.

## 7. Architecture changes made

None. Gate 6 was a pure verification pass — no field IDs, formulas, or values
were added or changed. This is itself a positive signal: the extraction held up
under independent re-verification without needing correction.

## 8. Remaining blockers (updated 2026-07-21)

D-014 EBITDA sign-off — **ratified 2026-07-21**, user approved as recommended,
no adjustments (see decision_log.md and EBITDA_DEFINITION_MEMO.md §6). User
thesis doc (Q-06) — **resolved 2026-07-21** via clarifying questions; see
D-018 and `01_Research_Outputs/ORCL_User_Thesis_and_Questions.docx`; Gate 8 no
longer blocked on this. Still open: transcripts (Q-04) and analyst-day deck
(Q-05) still missing; preferred-stock conversion terms (Q-11); SRC-016
capture defect (cosmetic, non-blocking); the four documented blocked checks
(§4).

## 9. Exact next prompt (Gate 7)

> Continue the Oracle equity-research project. This session is Gate 7:
> forecast-driver design. Read CLAUDE.md, CURRENT_STATE.md, 00_project_control/
> (especially GATE_6_REVIEW.md and the now-closed conflict register), the
> historical architecture and reconciliation docs, and the full extraction files
> in 10_Working_Data/raw_extractions/. Using the validated FY2025–FY2026
> historical base, triage the Framework's substantive modeling unknowns (Q-18
> open-questions family D) into answerable-from-filings vs. permanently
> assumption-based, and design the explicit driver set for the FY2027 Q1 – FY2028
> Q4 forecast (revenue streams, margin structure, capacity/capex mechanics,
> financing and dilution mechanics) per the project's forward comparable-company
> valuation objective. Do not begin scenario approval (Gate 8, requires explicit
> user sign-off on the scenarios themselves — the thesis doc, Q-06, was resolved
> 2026-07-21 per D-018 and no longer blocks it), comps methodology (Gate 9), or
> any model build. Update project-control files, commit, and push on the
> designated branch.
