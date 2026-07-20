# Project Scope — Oracle (ORCL) Equity Research & Valuation Model

Established: 2026-07-20 (from user brief; operational rules live in root `CLAUDE.md`)

## Objective

Build an institutional-quality, auditable Oracle operating forecast and relative
valuation model producing quarterly bear, base, and bull implied share prices:

1. Eight-quarter operating forecast, FY27 Q1 (Aug 2026 quarter) through FY28 Q4
2. Price targets at Oracle's next four earnings releases, beginning FY27 Q1
   (expected 2026-09-10)
3. Bear / base / bull operating cases, operationally distinct (not ±10% haircuts)
4. Comparable-company valuation on forward (NTM) metrics
5. Explicit linkage: operating performance → financing requirements → per-share equity value
6. Subsequent evaluation of whether ORCL stock or options offer attractive risk-adjusted
   returns (deferred to Gate 15; instrument choice depends on the user thesis document)

This is not a stock pitch. The standard is the research framework an equity-research
analyst would build before committing capital.

## Why this project exists

Oracle sits in a tension between rapid OCI/AI-infrastructure growth (FY26 revenue $67.4B,
exit RPO reported at $638B) and the cost of serving it: FY26 capex ~$55.7B, negative free
cash flow (~ −$23.7B FY26), gross debt ~$130–135B (see conflict C-01), large uncommenced
lease commitments (unverified, C-06), a $20B ATM equity program with reflexive-dilution
risk, and heavy AI-customer concentration. FY27 guidance (~$90B revenue, ~$70B net cash
capex, ~$40B financing) implies OCI roughly doubling.

The model must determine what operational and financial outcomes are required for the
stock to work, distinguishing at every step between: signed demand, available capacity,
revenue recognition, accounting earnings, cash generation, financing requirements, and
per-share equity value. **Rapid revenue growth is not assumed to create equity value.**

## Central modeling question

How much durable common-equity value does Oracle create after paying for capacity,
depreciation, leases, interest, preferred dividends, and common-share dilution?

## Analytical architecture (candidate, to be ratified at Gate 4/7)

The Eight-Quarter Model Framework document (`01_Research_Outputs/`) proposes, and this
project provisionally adopts pending Gate 4 ratification:

- Six-stream revenue recast: OCI · cloud applications · software support · software
  licenses · hardware · services (OCI and apps split out of reported "cloud services and
  license support")
- Capacity-based OCI forecasting (capacity index × utilization × revenue/unit), not
  growth-rate extrapolation; RPO treated as a demand indicator, not a revenue forecast
- Separate tracking of gross capex vs. customer prepayments vs. BYOH vs. short-term
  financing vs. net cash capex; depreciation by vintage
- Primary valuation: EV/NTM EBITDA with capital-adjusted controls; cross-checks via
  P/NTM EPS, shadow SOTP, and FCF analysis
- Peer set: MSFT/AMZN/GOOGL (infrastructure), SAP/CRM/NOW (applications), IBM (mature),
  CRWV (reference-only); weighting is an open Gate 9 decision

## Deliverables

- Reconciled quarterly historical dataset with full source lineage
- Excel model (control panel, scenario switch, quarterly valuation engine, checks tab)
- Per-earnings-date bear/base/bull price targets with milestone-based multiple logic
- Investment interpretation memo (stock vs. options, risk-adjusted)

## Out of scope

- Trading execution or live portfolio actions (the DK Money Agent brokerage connector in
  this workspace is not to be used for order placement as part of this project)
- Product-level SaaS P&Ls (Fusion/NetSuite/Health) beyond KPI overlays — insufficient
  disclosure
- Price targets beyond the four specified earnings dates
