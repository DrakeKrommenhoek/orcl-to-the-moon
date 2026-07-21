# Gate 9 Review — Comps Methodology

Date: 2026-07-21 · Session scope: settle the comparable-company methodology
questions carried since Gate 4 (Q-12, Q-14), choose the primary valuation
method, and determine what's blocked pending live market data. Branch:
`claude/oracle-historical-extraction-handoff-7dn6cr`.

Full deliverable: `11_Analysis/valuation/GATE9_COMPS_METHODOLOGY.md`.

## 1. What this gate produced

1. **Primary valuation method:** EV/NTM EBITDA with five mandatory capital-
   adjusted controls (capex/revenue, EBITDA-less-capex, OCF-less-capex,
   lease-adjusted net leverage, incremental ROIC) — chosen so EBITDA's
   blindness to capex intensity can never silently make an uneconomic
   capacity build look attractive in the primary output.
2. **Peer set and weighting (Q-14 resolved):** business-line peer mapping
   adopted from the Framework; the two AI research sources' Amazon/Alphabet
   disagreement resolved by weighting (Microsoft ~50%, Amazon ~25%, Alphabet
   ~25% within the OCI reference) rather than a binary include/exclude call,
   since both sources agreed on inclusion and differed only on emphasis.
   CoreWeave confirmed reference-only.
3. **NTM-window alignment (Q-12 resolved):** calendar-quarter basis for every
   company (Oracle and peers alike), resolving the fiscal-year-end mismatch
   (C-10) without restructuring Oracle's own fiscal-quarter forecast.
4. **Explicitly not adopted:** the Framework's bear/base/bull multiple ranges
   — carried forward as a Gate 13 candidate only, since real multiple
   assignment needs live peer market data.
5. **C-09 confirmed still blocked:** the existing comp table (prices, EVs,
   NTM estimates) is single-sourced and stale; re-sourcing needs either
   FactSet authentication or user-supplied data. This is a genuine external
   blocker, not resolved by design work, and is not fabricated from model
   knowledge.

## 2. User decision

**Approved all three methodology recommendations (§1-3 above) as proposed,
no adjustments.** Logged as **D-021** in `decision_log.md`.

## 3. What remains open

- Q-08 (consensus/live market-data source) and C-09 (comp table re-sourcing)
  — both block Gate 13's actual multiple assignment and per-share output.
- Q-11 (preferred-security treatment) — flagged as a live dependency for the
  P/NTM EPS cross-check.
- Hardware/services peer gap (thin IBM-only proxy) — revisit at Gate 13 if a
  more precise comp is needed.
- Q-04/Q-05 (transcripts/analyst day) — open, non-blocking.

## 4. Next step (Gate 10 — minimal model build)

Gate 10 can now start: the ratified historical dataset (Gate 6), driver
architecture (Gate 7), ratified scenario ranges (Gate 8, D-020), and this
gate's methodology (D-021) are all in place. Per CLAUDE.md's Excel standards,
Gate 10 is a *minimal* build — historical actuals, one scenario switch, and a
checks tab wired correctly — not the full 12-tab structure (that's Gate 12).
Actual EV/NTM EBITDA multiple assignment and per-share targets stay deferred
to Gate 13 pending Q-08/C-09.
