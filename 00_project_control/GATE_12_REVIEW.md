# Gate 12 Review — Full Model Build

Date: 2026-07-21 · Session scope: extend the Gate 10/11 minimal build with
capex/depreciation, debt/lease/cash mechanics, diluted shares, and a cash-flow/
returns tab carrying D-021's five capital-adjusted valuation controls. Branch:
`claude/oracle-historical-extraction-handoff-7dn6cr`.

Deliverable: `12_Model/development/ORCL_8Q_Model_v0.3_Gate12.xlsx` (v0.2
archived unchanged to `12_Model/archived_versions/` first).

## 1. What this gate added

Four new tabs, plus historical anchor rows and one re-link:

1. **Capex & Depreciation** — gross/net cash capex (scenario-selected per
   D-020; FY28 net cash capex has no ratified figure, so gross capex is used
   as an explicitly-labeled proxy), depreciation (PP&E) split from
   amortization of intangibles for the first time (Gate 10's EBITDA used a
   single combined envelope). Depreciation's quarterly shape reuses the real
   FY26 acceleration pattern (17.7%/22.4%/28.2%/31.7%); amortization has no
   ratified range and is held flat at the FY26 actual, spread evenly (FY26's
   own quarters were ~25% each — a real, not fabricated, pattern).
2. **Debt, Leases & Cash** — debt roll-forward anchored to the FY26 Q4 actual
   (added to Historical Actuals) with the D-020 scenario-selected ending
   debt; net issuance is an explicit plug, not a security-by-security build,
   because no issuance schedule is disclosed (Gate 7 §2 item 22). Interest
   expense pulls the scenario-selected annual figure, spread evenly (no
   disclosed quarterly seasonality for interest). The lease-commencement
   schedule spreads the disclosed $260B uncommenced-lease pool (C-06) evenly
   across the FY2027-FY2029 window the FY26 10-K actually states — a
   simplification flagged in the workbook, since no finer schedule exists.
   Ending cash follows the same scenario-selected-endpoint-plus-plug pattern.
3. **Equity & Shares** — diluted shares pull the D-020 scenario-selected
   figure directly rather than being re-derived from an assumed ATM issuance
   price, because Gate 7 flagged ATM pricing as reflexive with the (not yet
   computed) valuation output — deriving shares from a guessed price here
   would be circular.
4. **Cash Flow & Returns** — implied operating cash flow is solved as a plug
   from the cash identity (`Beginning cash + OCF − net cash capex + net debt
   issuance = Ending cash`), explicitly labeled as a reconciling figure that
   absorbs dividends/buybacks/other items not separately modeled, not a
   bottom-up forecast. Carries four of D-021's five mandated EV/NTM-EBITDA
   controls: capex/revenue, EBITDA-less-capex, OCF-less-capex (=FCF), and
   lease-adjusted net leverage. The fifth (incremental ROIC) is explicitly
   **not built** — it needs an invested-capital base beyond Gate 12's
   balance-sheet scope, deferred to Gate 13.

Margin & EBITDA's D&A line (row 11) was re-linked from the old combined
envelope to the new split Depreciation + Amortization build — a real fidelity
improvement, not just an addition.

Checks tab gained CHECK_080 (debt roll-forward) and CHECK_100 (cash tie) —
both true by construction (the plugs are defined to make them tie), so they
document the identity and confirm correct wiring rather than independently
validating the forecast; the workbook says this explicitly rather than
overclaiming what a green check means.

## 2. Independent verification

Same method as Gates 10/11 (LibreOffice recalculation remains broken in this
sandbox — not re-tested this gate, already confirmed twice). A full-chain
Python replica of the Base scenario across every new mechanic was run outside
the workbook:

- FY27: EBITDA ~$45.1B, implied OCF ~$43.3B, FCF ~-$26.7B, lease-adjusted
  leverage ~5.4x
- FY28: EBITDA ~$71.8B, implied OCF ~$90.5B, FCF ~-$17.0B, lease-adjusted
  leverage ~4.8x (declining from FY27, consistent with the Framework's own
  base-case narrative that "leverage peaks before declining as FY28 revenue
  scales")

FCF stays deeply negative in both years — consistent with the project's
central question (how much cash generation is required to fund the buildup)
rather than an artifact of a broken formula. All cross-sheet references
re-verified as correctly quoted (zero unquoted multi-word references) after
every change.

## 3. What Gate 12 still does not build

Incremental ROIC (D-021 control 5); a true debt-instrument-level issuance
schedule (net issuance stays a plug); a finer lease-commencement schedule
than an even three-year spread; dividends/buybacks as separately modeled
cash-flow lines (bundled into the OCF plug); the GAAP-operating-margin gap
flagged at Gate 10 (still held flat at the FY26 actual — no ratified range
exists for that specific line). These are candidates for Gate 13 (valuation)
or a future refinement pass, not omissions from carelessness — each is
labeled in the workbook itself.

## 4. Next step (Gate 13 — valuation)

Gate 13 can now: assign real EV/NTM EBITDA and P/NTM EPS multiples (pending
Q-08/C-09 — still blocked without live peer market data or an explicit
user-approved assumption set); compute NTM EBITDA/EPS at each of the four
valuation dates using the walk-forward mechanic (Framework §14); build the
enterprise-to-equity bridge (Framework §15, pending Q-11's preferred-security
treatment and Q-13's lease-in-EV convention); and produce the bear/base/bull
per-share price targets this whole project exists to deliver.
