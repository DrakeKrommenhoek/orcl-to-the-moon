# Gate 14 Review — Sensitivities

Date: 2026-07-21 · Session scope: produce the bear/base/bull price range and
multiple sensitivity the project's central objective calls for, using the
illustrative multiple explicitly (per the user's instruction — "proceed to
Gate 14 with the illustrative multiple"). Branch:
`claude/oracle-historical-extraction-handoff-7dn6cr`.

Deliverable: `12_Model/development/ORCL_8Q_Model_v0.5_Gate14.xlsx` (v0.4
archived first).

## 1. What this gate added

**"Sensitivities (Gate 14)" tab**, four sections, all carrying the same
ILLUSTRATIVE-ONLY labeling as the Valuation tab (still true: no real,
sourced multiple exists — Q-08/C-09 unresolved):

1. **Bear/Bull NTM revenue by stream**, computed directly from the Scenario
   Assumptions Bear/Bull columns rather than the single Control-Panel switch
   (which only drives one case at a time) — same closed-form logic the Base
   case already uses (growth applied to the FY26 actual, spread by the same
   empirical seasonality shares), just substituting each scenario's own
   growth range.
2. **Bear/Bull NTM D&A and EBITDA** — depreciation differs by scenario
   (D-020's own ranges); amortization, GAAP operating margin, and effective
   tax rate do not (no ratified scenario range exists for those lines in any
   scenario, so they're held flat across Bear/Base/Bull too — the same
   documented gap from Gates 10-13, not a new one introduced here).
3. **Bridge components by scenario** (debt, cash, shares each pull their own
   D-020 ending range; lease liabilities and preferred stay scenario-flat,
   since the lease-commencement schedule is a fixed disclosed timeline and
   preferred is held at its FY26 actual regardless of case).
4. **The bear/base/bull illustrative price table** — the actual triad the
   whole project exists to produce. At the FY27 Q1 valuation date, using the
   Framework's own unadopted candidate multiple midpoints (Bear 10.0x, Base
   13.0x, Bull 16.0x EV/NTM EBITDA): **Bear ~$96/share, Base ~$166/share,
   Bull ~$244/share** — correctly ordered (bear < base < bull), verified
   independently in Python before and after wiring the formulas.
5. **One-way multiple sensitivity table** — holds the Base case's NTM EBITDA
   and bridge fixed, varies the multiple from 9x to 17x, showing how the
   illustrative price moves with the multiple alone.

## 2. Independent verification

Same method as prior gates. A full Python replica of the Bear/Bull NTM
revenue, D&A, EBITDA, bridge, and price calculations was run outside the
workbook and matches the formulas traced from the actual file: Bear
$96.22/share, Bull $244.44/share (Base $165.57/share, from Gate 13). The
monotonic ordering (bear < base < bull) is a meaningful sanity check — a
broken formula chain would be far more likely to produce a nonsensical
ordering than to accidentally preserve it. Zero unquoted cross-sheet
references, re-checked after every edit.

## 3. What this gate deliberately simplified

This is a **single-valuation-date, closed-form approximation** (FY27 Q1
only), not a full triplicated quarterly rebuild of Bear/Bull across all four
valuation dates — building that out would mean tripling the Revenue Forecast
and Margin & EBITDA tabs' quarterly mechanics. The tab says this directly.
Extending to all four valuation dates, or building true parallel quarterly
scenario columns instead of the single-switch architecture, is a reasonable
next refinement but not required to deliver the bear/base/bull range the
project's central objective calls for.

## 4. What remains genuinely blocked

Everything in this gate still rests on the Framework's own **unadopted**
candidate multiples, not a sourced one. The moment Q-08 resolves (FactSet
authenticated, or the user supplies current peer market data), the same
mechanism here — and on the Valuation tab — should be re-run with real
multiples in place of the illustrative midpoints, and only then does the
output stop being illustrative and become an actual investment input.

## 5. Next step (Gate 15 — investment interpretation)

Gate 15 can now draft the investment-interpretation memo structure (stock vs.
options, risk-adjusted) using the illustrative bear/base/bull range as a
stand-in for the real one, with the same "illustrative, not final" caveat
carried through — or wait until Q-08 resolves so the memo can use real
numbers from the start. Either way, the mechanical scaffolding this project
needs (historical data → forecast drivers → scenarios → comps methodology →
full model → valuation → sensitivities) is now complete end-to-end.
