# Gate 13 Review — Valuation

Date: 2026-07-21 · Session scope: build the NTM aggregation, enterprise-to-
equity bridge, and Net Income/EPS mechanics; leave real multiple assignment
explicitly blocked pending Q-08/C-09, per the user's instruction to "continue
into Gate 13 with what's buildable, flag the rest." Branch:
`claude/oracle-historical-extraction-handoff-7dn6cr`.

Deliverable: `12_Model/development/ORCL_8Q_Model_v0.4_Gate13.xlsx` (v0.3
archived unchanged first).

## 1. What this gate added

**Net Income & EPS bridge** (Margin & EBITDA tab, extending the operating-
income build that stopped short in Gate 10/12): interest expense (linked
from the Debt tab) less GAAP operating income gives pre-tax income; a
trailing FY26 effective tax rate (12.6%, held flat — no ratified scenario
range exists for tax rate any more than for GAAP operating margin) gives
GAAP net income; preferred dividends (held flat at the FY26 Q4 actual rate,
$81mm/quarter, under Q-11's unresolved debt-like default) are subtracted to
get net income available to common; divided by diluted shares (Equity &
Shares tab) gives GAAP diluted EPS.

**Valuation (Gate 13) tab**, four sections:

1. **NTM aggregation** at exactly the four dates the Framework specifies
   (Q-07: FY27 Q1 release 2026-09-10 through FY27 Q4 release, each with its
   stated NTM window) — summed directly from the Revenue Forecast, Margin &
   EBITDA, and new EPS build. No new methodology here; this is mechanical
   aggregation of what Gates 10-13 already built.
2. **Enterprise-to-equity bridge components** (gross debt, on-balance-sheet
   lease liabilities, preferred, cash + marketable securities) pulled at the
   balance as of the quarter just completed at each valuation date — using
   the Debt, Leases & Cash tab's quarterly interpolations. Preferred is
   subtracted (debt-like, Q-11's unresolved default) and leases are included
   (Q-13's lease-in-EV convention is also unresolved — flagged directly on
   the tab as something to verify before this bridge is signed off).
3. **Multiple assignment — left genuinely blank.** These cells are
   highlighted yellow and empty by design: assigning a real EV/NTM EBITDA or
   P/NTM EPS multiple needs live, as-of-dated peer market data (Q-08's
   FactSet connector is still unauthenticated; C-09 already flags the
   existing comp table as stale and single-sourced). Filling these from an
   LLM's general knowledge of current prices/multiples would be exactly the
   kind of unlabeled estimate the project's data-integrity rules prohibit —
   so the cells stay blank for the user or an authenticated source to fill.
4. **Illustrative-only mechanism demonstration**, clearly marked in red and
   explained in the tab's own header note, using the Framework's own
   explicitly-unadopted candidate base-case multiple (12x-14x EV/NTM EBITDA,
   midpoint 13.0x) purely to prove the bridge computes something sane, not as
   a price target. At the first valuation date (FY27 Q1 release), this
   produces an illustrative $165.57/share — the same order of magnitude as
   the user's own $150 thesis target, which is a useful sanity signal that
   nothing in the mechanism is structurally broken, not a claim that $165.57
   is a real number.

## 2. Independent verification

Same method as prior gates (LibreOffice recalculation still unavailable in
this sandbox). A full-chain Python replica of the entire Base-scenario
pipeline — revenue streams through NTM aggregation through the equity bridge
— was run outside the workbook and matches the formulas traced from the
actual file cell-by-cell (same NTM revenue/EBITDA, same bridge components,
same illustrative price). Zero unquoted cross-sheet references, re-checked
after every edit.

## 3. What Gate 13 did not do (and why)

- **No real multiple was assigned.** This is the one genuine external block
  in the whole project plan — not a design choice deferred by preference.
- **Incremental ROIC** (D-021's fifth control) still not built — needs an
  invested-capital base beyond what Gate 12 built.
- **The GAAP-operating-margin and effective-tax-rate lines** remain held
  flat at FY26 actuals rather than scenario-switched — no ratified D-020
  range exists for either. A future gate should either derive them from the
  historical bridges already in the model or get them explicitly ratified.
- **Q-11 (preferred treatment) and Q-13 (lease-in-EV convention)** are used
  with their stated defaults (debt-like, leases-included) but remain formally
  unresolved — the Valuation tab says so directly rather than presenting the
  bridge as settled.

## 4. Next step

The model is now structurally complete end-to-end (revenue → margin → EBITDA
→ net income/EPS → cash flow → NTM aggregation → equity bridge) except for
the one number that requires external data: the multiple. Next session
should either (a) get Q-08 resolved — FactSet authentication or user-
supplied as-of-dated peer comps — and complete Gate 13's multiple assignment
for a real price target, or (b) proceed to Gate 14 (sensitivities) using the
illustrative multiple purely to test the model's mechanical sensitivity to
scenario/driver changes, with the same "illustrative, not a real output"
labeling carried through.
