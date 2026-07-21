# Gate 7 Review — Forecast-Driver Design

Date: 2026-07-21 · Session scope: design the explicit driver set for the
FY2027 Q1 – FY2028 Q4 forecast (revenue streams, margin structure, capacity/
capex mechanics, financing/dilution mechanics) and triage the Framework's 30
substantive modeling unknowns (§16), per the Gate 6 restart prompt. Branch:
`claude/oracle-historical-extraction-handoff-7dn6cr`.

Full deliverable: `11_Analysis/forecast/GATE7_FORECAST_DRIVER_DESIGN.md`.

## 1. What this gate produced

1. **Empirical seasonality table** (§1 of the driver doc) — quarter-share-of-FY
   computed directly from the Gate 6 reconciled historical file for all six
   Layer 3 revenue streams, both fiscal years. Real finding, not an assumption:
   license revenue is consistently ~39-40% Q4-weighted in both years; support
   revenue is essentially flat quarter to quarter (±1%); OCI's Q4 weighting
   grew from 29.3% (FY25) to 32.0% (FY26), consistent with capacity additions
   concentrating late in the year.
2. **Triage of all 30 Framework §16 questions** into: 8 permanently
   assumption/scenario-input by design (customer-level RPO mix, capacity-unit
   economics, ATM pricing, future debt terms, etc.); 10 partially answerable
   from documents already in the repo (short list of FY26 10-K footnote
   re-reads before Gate 10, not new document requests); 2 that need a specific
   new document/connector already tracked (Q-11 preferred terms, Q-08
   consensus source); the remainder resolved or bounded by data already
   extracted (effective tax rate, support-revenue stability, aggregate
   prepayment/BYOH figures).
3. **Explicit forecast driver formula for each of the six revenue streams**,
   distinguishing real calibratable inputs (historical growth, seasonality,
   RPO conversion) from assumption slots with no disclosed unit to calibrate
   against (capacity/utilization/revenue-per-unit for OCI; units×ASP for
   hardware; headcount×rate for services).
4. **Capacity contribution index (Q-15) provisional definition (D-019)** —
   a relative, unitless index rebased to FY26 Q4 = 100, built from net PP&E
   growth attributable to the buildout, reconciled against disclosed site/RPO/
   lease-commencement anchors. Issued in the same "analyst proposes, user
   ratifies" pattern as D-014; does not block Gate 8.
5. **Depreciation-by-vintage, debt roll-forward, lease-commencement, ATM/
   dilution, and preferred-security mechanics** — each keyed to existing field
   IDs, with the genuinely reflexive driver (ATM issuance price ↔ valuation
   output) flagged explicitly rather than modeled as a one-way calculation.
6. **Valuation checkpoint scaffolding** (four dates, NTM windows, walk-forward
   mechanic) reproduced from Framework §14 and tied to the VAL_ fields already
   reserved in the data dictionary.

## 2. What this gate deliberately did not do

- Did not assign any scenario numeric range (Gate 8 — requires explicit user
  sign-off per CLAUDE.md; Framework §10's ranges are carried forward as a
  candidate starting point only, not adopted).
- Did not choose peer set, weighting, or NTM-alignment convention (Gate 9 —
  Q-12, Q-14).
- Did not build any Excel/model artifact (Gate 10+).
- Did not resolve Q-08, Q-11, Q-13 — cross-referenced where they touch a
  driver mechanic, left open.

## 3. New field IDs introduced

None. Per architecture §14, forecast quarters populate the same field set
(REV_310-370, COGS/OPEX/PROF, CF, DEBT, SHARE, CAP, VAL_ fields already
reserved) with `historical_or_forecast = forecast`. This gate designed the
*population rule* for forecast periods, not new fields.

## 4. Decisions logged

**D-019** (provisional): capacity contribution index definition (Q-15). See
`decision_log.md` and driver-doc §4.

## 5. Remaining blockers into Gate 8/9

Unchanged: Q-04 (transcripts), Q-05 (analyst-day deck), Q-08 (consensus
source), Q-11 (preferred treatment — needs Certificate of Designations/
prospectus), Q-12 (NTM alignment), Q-13 (lease convention), Q-14 (peer
weighting). New, non-blocking: four targeted FY26 10-K footnote re-reads
(useful lives, capitalized interest, BYOH treatment, nonoperating investments)
recommended before Gate 10, listed in driver-doc §7.

## 6. Exact next prompt (Gate 8)

> Continue the Oracle equity-research project. This session is Gate 8:
> scenario approval. Read CLAUDE.md, CURRENT_STATE.md, 00_project_control/
> (especially this file and open_questions.md), the filled-in user thesis
> (`01_Research_Outputs/ORCL_User_Thesis_and_Questions.docx`, D-018), and
> `11_Analysis/forecast/GATE7_FORECAST_DRIVER_DESIGN.md`. Present the
> Framework's §10 bear/base/bull numeric ranges (OCI growth, applications
> growth, margins, capex, depreciation, debt, cash, diluted shares for FY27
> and FY28) to the user for explicit review against their stated thesis
> ($150 year-end target via multiple expansion, 6-18 month hold, long calls),
> and record the user's approval or adjustments as a new ratified decision.
> Do not begin comps methodology (Gate 9) or any model build (Gate 10) in this
> session. Update project-control files, commit, and push on the designated
> branch.
