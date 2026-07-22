# Gate 11 Review — Model Checks

Date: 2026-07-21 · Session scope: strengthen the Gate 10 minimal build's
integrity checks with what's actually buildable before Gate 12 adds the
balance-sheet/cash-flow schedules, and re-attempt LibreOffice recalculation.
Branch: `claude/oracle-historical-extraction-handoff-7dn6cr`.

Deliverable: `12_Model/development/ORCL_8Q_Model_v0.2_Gate11.xlsx` (v0.1
archived unchanged to `12_Model/archived_versions/` per CLAUDE.md's
model-versioning rule before this session's edits).

## 1. What this gate added

**CHECK_090 — GAAP/non-GAAP operating income bridge**, historical quarters
only. Historical Actuals gained three new rows (OPEX_040 amortization of
intangibles, OPEX_070 stock-based compensation, and a combined acquisition-
related + restructuring row — using OPEX_065's combined caption for FY26 Q4,
where OPEX_050/060 aren't filed separately, per the D-013 dual-presentation
bridge). The Checks tab re-derives `(Non-GAAP operating income − GAAP
operating income)` and compares it against `(SBC + amortization +
acquisition/restructuring)` for all 8 historical quarters. This is a genuine
second-source check, not a tautology — PROF_030 (non-GAAP operating income)
was originally extracted directly from each release's own non-GAAP
reconciliation table, while this check rebuilds the same number bottom-up
from the individually filed reconciling-item lines. **Confirmed to tie within
$1mm rounding in all 8 quarters** before wiring the formula into the
workbook (verified independently in Python, then structurally re-verified
against the actual cell values after writing the formulas).

## 2. LibreOffice recalculation — retried, still broken

Re-attempted `scripts/recalc.py` against a fresh copy of the v0.1 workbook
with a 290s budget. **Same hang as Gate 10** — confirms this is a persistent
sandbox limitation, not a one-off. No further attempts planned this session;
noted again in `CURRENT_STATE.md` for whichever future session/environment
can actually run it (or for the user to confirm after opening the file
themselves, which is the normal path for any script-written workbook's first
calculation regardless of this issue).

## 3. Structural verification performed (in lieu of live recalculation)

1. Zero-count check for unquoted multi-word cross-sheet references (would be
   a silent `#VALUE!` in real Excel) — none found, including in the new
   CHECK_090 formulas.
2. Independent Python evaluation of the CHECK_090 formula against the actual
   cell values written into the workbook (not just the pre-write Python
   sanity check) — variances of 0 or 1 ($mm) across all 8 quarters, matching
   the pre-write verification exactly.

## 4. What Gate 11 did not add (correctly deferred)

Balance-sheet ties, cash-flow ties, and a forecast-side GAAP/non-GAAP bridge
all require schedules that don't exist yet (debt, leases, capex, cash) — that
is Gate 12 (full build) scope. Adding placeholder checks against
not-yet-built schedules would just be checks that can never pass; better to
add them once the schedules exist.

## 5. Next step (Gate 12 — full build)

Gate 12 should add: debt/lease roll-forward, depreciation-by-vintage (once
D-019's capacity index is confirmed), ATM/dilution mechanics, diluted share
build, and the balance-sheet/cash-flow schedules — at which point Gate 11's
Checks tab should be revisited to add CHECK_080 (debt roll-forward),
CHECK_100 (cash tie), and a forecast-side GAAP/non-GAAP bridge. The
GAAP-operating-margin gap flagged at Gate 10 (§3 of `GATE_10_REVIEW.md`)
should also be closed at Gate 12.
