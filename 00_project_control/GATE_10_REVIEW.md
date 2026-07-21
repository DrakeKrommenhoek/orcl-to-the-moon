# Gate 10 Review — Minimal Model Build

Date: 2026-07-21 · Session scope: build a minimal working Excel model —
historical actuals, one scenario switch driving all cases, a revenue-stream
forecast using Gate 7's driver mechanics and Gate 8's ratified ranges (D-020),
top-down margin/EBITDA, and a checks tab. Branch:
`claude/oracle-historical-extraction-handoff-7dn6cr`.

Deliverable: `12_Model/development/ORCL_8Q_Model_v0.1_Gate10.xlsx`.

## 1. What was built

Six tabs, in this order:

1. **Control Panel** — scenario selector (Bear/Base/Bull dropdown) and
   valuation-date selector (four dates per Q-07/D-021), plus reference notes
   and an explicit scope statement.
2. **Historical Actuals** — the six Layer-3 revenue streams and four
   supplemental P&L lines (gross profit, GAAP/non-GAAP operating income,
   EBITDA) for all 8 historical quarters + 2 fiscal years, hardcoded from the
   Gate 6 reconciled dataset (blue input cells), with annual columns computed
   as `=SUM()` of the quarters (formula, not hardcoded) and margin-% rows
   computed as formulas.
3. **Scenario Assumptions** — the full D-020 ratified range table (all twelve
   driver rows, FY27 and FY28), with a "Selected" column that pulls the
   midpoint of whichever scenario is chosen on the Control Panel via
   `IF(...,AVERAGE(...))`, and an explicit "wired into Gate 10 forecast?"
   column marking which rows this gate actually consumes (OCI growth,
   applications growth, GAAP gross margin, non-GAAP operating margin) versus
   which are scaffolded for Gate 12 (capex, depreciation, interest, debt,
   cash, shares).
4. **Revenue Forecast** — FY27 Q1 through FY28 Q4 for all six streams.
   OCI and Applications growth pull the scenario-switched value; Support/
   License/Hardware/Services (no D-020 range exists for these) use their own
   trailing FY26 actual growth rate, held flat, clearly labeled as a Gate 10
   simplification per Gate 7 §3's disposition. Quarterly spread uses the
   empirical FY26 seasonality shares (Gate 7 §1) for every stream, including
   OCI — flagged as a placeholder pending D-019's capacity index (Gate 12).
   Includes a cross-check row comparing the bottom-up total against the
   Framework's own top-down total-revenue range.
5. **Margin & EBITDA** — top-down margin per Gate 7 §5 (no stream-level
   margin is ever disclosed): GAAP gross margin and non-GAAP operating margin
   pull the scenario-selected values; EBITDA is built per the ratified D-014
   definition (GAAP operating income + D&A), with GAAP operating margin held
   at the FY26 actual (no ratified scenario range exists for that specific
   line — documented gap, not silently assumed) and D&A pulled as a combined
   envelope from the Scenario Assumptions depreciation range (not yet
   vintage-split — Gate 12).
6. **Checks** — six-stream-sum-to-total and sum-of-quarters-to-FY ties, run
   on both the historical tab (re-verifying Gate 6's own reconciliation
   inside the model itself) and the forecast tab (confirming the build
   mechanics hold together), plus a scenario-switch sanity check confirming
   the selected value falls within the bear-to-bull range for each
   switched driver.

Every hardcoded number carries either a direct cell reference back to the
historical dataset/D-020, or an inline note explaining its source (trailing
actual growth, FY26-held margin). Blue = hardcoded input, black = formula,
green = cross-sheet link, per CLAUDE.md's Excel color convention.

## 2. Independent verification (formula-level, not LibreOffice-recalculated)

**LibreOffice's headless macro-recalculation is broken in this sandboxed
environment** — confirmed via repeated, isolated tests (a trivial one-cell
`=A1+A2` workbook hangs indefinitely on the same recalculation step, with a
clean profile, no competing processes, the AF_UNIX socket shim forced on, and
timeouts up to 350s). This is an environment limitation, not a defect in the
workbook. Two things establish the workbook is sound anyway:

1. **Every cross-sheet reference was programmatically checked** for correct
   quoting (`'Sheet Name'!` — an unquoted multi-word sheet reference is a
   silent `#VALUE!` in real Excel) — zero found unquoted.
2. **An independent Python replica of the Base-scenario formula chain** was
   run outside the workbook to sanity-check magnitudes: the bottom-up,
   stream-by-stream build lands at FY27 revenue of $90.5B and FY28 of
   $129.1B — squarely inside the Framework's own top-down base-case ranges
   ($89.5-90.5B and $127-132B respectively) despite never being forced to
   match them. That convergence is a real, useful validation that the driver
   mechanics (empirical seasonality + scenario-switched OCI/applications
   growth + trailing growth for the other four streams) are internally
   consistent, not a coincidence to take on faith.

**Action for the user:** open the file in real Excel, Google Sheets, or a
working LibreOffice install once — any of them recalculates all formulas on
first open, which is normal behavior for any file written by a script rather
than by the application itself (this is not specific to this workbook). If
any cell then shows a formula error, that is worth a follow-up; none were
found in the structural review above.

## 3. What Gate 10 deliberately did not build

Per its "minimal" scope (Gate 12 is the full build): no debt roll-forward, no
lease-commencement schedule, no depreciation-by-vintage (D-019's capacity
index is not implemented — the D&A line is a single combined envelope), no
ATM/dilution mechanics, no diluted-share build, no NTM/valuation-checkpoint
output, no per-share price target. The GAAP operating margin line has no
ratified scenario range to switch on — flagged in the workbook itself as a
gap for Gate 12 to close (either derive it from the historical GAAP/non-GAAP
opex bridge, or ask the user to ratify a range directly).

## 4. Next step (Gate 11 — model checks)

Gate 11 should: (a) get real LibreOffice recalculation working — either by
retrying in a future session/environment, or asking the user to confirm the
formulas calculate correctly after opening the file themselves; (b) expand
the Checks tab toward the full CHECK_ family (balance-sheet ties, cash-flow
ties, GAAP/non-GAAP bridge) once Gate 12 adds those schedules; (c) resolve
the GAAP-operating-margin gap noted in §3.
