# Gate 7 — Forecast-Driver Design

Gate: 7 · Date: 2026-07-21 · Status: complete (pending nothing — Gate 7 has no
required user sign-off; Q-15's capacity-index *definition* is issued here as a
provisional recommendation in the same pattern as D-014, to be ratified
alongside Gate 8)

Companions: `11_Analysis/historical/HISTORICAL_DATA_ARCHITECTURE.md` (structure
this gate extends), `10_Working_Data/architecture/orcl_data_dictionary.csv`
(field IDs used throughout — no new field IDs are introduced; forecast quarters
populate the same fields under `historical_or_forecast = forecast`),
`01_Research_Outputs/ORCL_Eight_Quarter_Model_Framework_2026-07-20.docx`
(source of the driver equations and the 30 unresolved questions triaged in §2).

## 0. Scope boundary (what this gate is and is not)

Gate 7 designs *how* each field will be forecast — the driver, its formula, its
inputs, and which inputs are real (filed/computable) vs. assumption slots. It
does **not**:
- Assign scenario numeric ranges (Gate 8 — requires explicit user sign-off).
- Choose comps, peer weighting, or NTM-window convention (Gate 9 — Q-12/Q-14).
- Build the Excel model (Gate 10+).
- Resolve Q-08 (consensus source), Q-11 (preferred treatment), or Q-13 (lease
  convention) — those stay open and are cross-referenced where they touch a
  driver, not decided here.

## 1. Historical seasonality (computed from actuals, per architecture §13)

Quarter-share-of-FY, computed directly from the Gate 6 reconciled historical
file (`orcl_historical_quarterly_full.csv`), REV_310–370:

| Stream | FY25 Q1/Q2/Q3/Q4 share | FY26 Q1/Q2/Q3/Q4 share |
|---|---|---|
| OCI (REV_310) | 21.0% / 23.8% / 25.9% / 29.3% | 18.5% / 22.5% / 27.0% / 32.0% |
| Cloud applications (REV_320) | 24.3% / 24.5% / 24.9% / 26.2% | 24.2% / 24.5% / 25.3% / 26.0% |
| Software support (REV_330) | 25.1% / 24.9% / 24.6% / 25.4% | 25.0% / 24.9% / 25.1% / 25.0% |
| Software license (REV_340) | 16.7% / 23.0% / 21.7% / 38.6% | 16.2% / 19.8% / 24.3% / 39.7% |
| Hardware (REV_350) | 22.3% / 24.8% / 23.9% / 29.0% | 21.7% / 25.2% / 23.2% / 30.0% |
| Services (REV_360) | 24.1% / 25.4% / 24.7% / 25.8% | 23.5% / 24.9% / 25.1% / 26.5% |
| Total (REV_370) | 23.2% / 24.5% / 24.6% / 27.7% | 22.2% / 23.8% / 25.5% / 28.5% |

Reading: license revenue is heavily Q4-loaded in both years (~39-40%,
consistent with Framework §2's "Q4 closing concentration" driver) — this is a
real, two-year-consistent pattern, not an assumption. OCI's Q4 weighting *grew*
from FY25→FY26 (29.3%→32.0%), consistent with capacity additions concentrating
late in the fiscal year; per architecture §13, **site-specific capacity timing
overrides this historical shape for OCI specifically** — the seasonality table
is a sense-check for OCI, not a mechanical forecast input. For the other five
streams (all demand/renewal-driven, not capacity-gated), historical seasonality
is a legitimate forecast input.

## 2. Triage of the Framework's 30 unresolved questions (§16)

Column "Class": **A** = answerable now from documents already in the repo
(flag for a targeted look, not a new document request); **B** = needs one
specific new document (transcript, analyst-day deck, prospectus) already
tracked as Q-04/Q-05/Q-11; **C** = will not be knowable before it happens —
permanently a scenario/assumption input, differentiated bear/base/bull per §7.

| # | Question | Class | Disposition |
|---|---|---|---|
| 1 | RPO % by major customer | C | Oracle discloses concentration only as "no customer ≥10%" (KPI_050); never breaks out RPO by customer. Stays qualitative risk factor, not a driver. |
| 2 | RPO % by OCI/apps/hardware/other | C | Never disclosed at that granularity. RPO_010 stays a single demand-indicator series (per C-07); do not decompose it by stream. |
| 3 | Termination/modification/minimum-usage rights | C | Not in filings; would need contract-level disclosure Oracle doesn't give. Qualitative bear-case risk only. |
| 4 | Customer prepayments/guarantees on largest commitments | A (partial) | Aggregate figures exist: $75B prepaid/BYOH (KPI_060), $4,592M FY26 prepayments (CAP_010), $3,345M short-term financing (CAP_020), a $3.3B lease guarantee (C-06 resolution note). Per-commitment detail is C. |
| 5 | Exact in-service dates for major sites | C | Not disclosed at site level. CIP (BS_050) and PP&E (BS_040) roll-forward are the only aggregate proxies. |
| 6 | Capacity mechanically complete but awaiting power/acceptance | C | No disclosure; qualitative bear/bull differentiator only (§7 scenario list already captures this as "power/construction/equipment delays"). |
| 7 | OCI revenue per MW/GPU/equivalent unit | C (by design) | Architecture §19 already rules this out — no capacity-unit disclosure exists. This is why Q-15's capacity index (§4 below) must be a relative, disclosure-anchored construct instead. |
| 8 | Utilization ramp for a new facility, first four quarters | C | One data point exists (KPI_030: "97.5% AI infra utilization" commentary, undated granularity) — insufficient for a ramp curve. Assumption, differentiated by scenario. |
| 9 | Gross margin by GPU-AI/database/multicloud/traditional | C (by design) | No stream-level margin ever disclosed (architecture §8/§16). COGS_310/320 stay structurally blank; margin must be derived top-down from consolidated gross margin (COGS_050/060), not built bottom-up. |
| 10 | BYOH accounting/depreciation treatment | A (partial) | FY26 10-K Note 4 (PP&E) likely addresses BYOH capitalization generally (SRC-024 was used for C-01/C-02/C-06 already) — worth a targeted re-read of Note 4's BYOH language before Gate 10, not a new document. |
| 11 | % of FY27 $90B revenue target from OCI | C | Not split by management publicly. Must be derived by the model itself (bear/base/bull OCI dollar forecast ÷ total), not sourced as a fact. |
| 12 | Management's internal FY28 applications-growth assumption | C | Not disclosed. FY26 actual growth (~11% per REV_135) is the empirical anchor; scenario spread per §7. |
| 13 | FY27 capex funded by prepay/BYOH/short-term financing | A (partial) | Management gave an aggregate framework (~$20-25B customer funding/timing per Framework §5) — this is guidance language, to be sourced/verified against the actual FY27 Q1 release/transcript when it arrives (2026-09-10), not treated as filed fact today. |
| 14 | % of FY27 capex remaining in CIP at year-end | C | No explicit guidance. BS_050 (CIP) historical trend ($16.5B FY25 Q4 → $40.0B FY26 Q4) is the only anchor; treat forward CIP-to-capex ratio as a scenario input. |
| 15 | Useful lives for GPUs/servers/network/DC infrastructure | A (partial) | FY26 10-K PP&E accounting-policy footnote almost certainly states useful-life ranges (standard 10-K disclosure) — flagged for a targeted footnote re-read before Gate 10 depreciation-by-vintage build; Framework §5's proposed ranges (GPUs/servers/networking 3-6yr; DC shell/power/cooling 15-40yr) are a reasonable placeholder pending that check, not yet filed-source-verified. |
| 16 | When will uncommenced leases enter the balance sheet | A (partial) | C-06's resolution already gives the aggregate commencement window ("FY2027 through FY2029", SRC-024 Note 9) — that is the real constraint on DEBT_070's roll-off. No further disclosure exists at a finer schedule; the *distribution* within FY27-FY29 is C. |
| 17 | PV of long-term lease commitments | C | Oracle discloses no discount rate for the $260B uncommenced-lease pool. A present-value estimate would be an analyst construct with an assumed discount rate — clearly labeled `assumed`, never `calculated` from a filed rate. |
| 18 | % of future capex that is maintenance vs. growth | C | Not disclosed; Oracle's capex is currently ~all growth by construction-in-progress trend. Assumption, scenario-differentiated. |
| 19 | Oracle's sustainable capex level after the current build | C | Forward-looking management commentary not yet available (would live in transcripts/analyst day, Q-04/Q-05, and even then it's guidance, not fact). |
| 20 | ATM execution price/pace | C (by design) | Genuinely market-dependent and reflexive (Framework §5) — this is the definition of a scenario input, not something to resolve. |
| 21 | Mandatory convertible EPS treatment | B → Q-11 | Needs the Certificate of Designations/prospectus terms (conversion ratio, trigger, mandatory conversion date). Already tracked as Q-11; not resolved here. |
| 22 | What debt instruments will fund FY27, at what coupons/maturities | C | Future issuance, unknown until it happens. Scenario input (rate/tenor assumptions), not a fact to chase. |
| 23 | Capitalized interest amount | A (partial) | Public company debt footnotes commonly disclose capitalized interest; worth a targeted check of the FY26 10-K interest/debt footnote before Gate 10 (same pass as #15/#10), not a new document. |
| 24 | Sustainable effective tax rate | A | Historical effective tax rate is a fully populated 8-quarter series (PROF_090) already in the reconciled dataset — use it as the empirical base-case anchor; forward guidance (if any) would refine it further via Q-04 transcripts. |
| 25 | How much more restructuring is required | C | Forward management decision, not disclosed. Scenario/assumption. |
| 26 | Could workforce reductions impair deployment | C | Qualitative risk, not a numeric driver. |
| 27 | Oracle Health revenue/margin/profitability | C (by design) | Architecture §19 already excludes product-level SaaS P&Ls as insufficiently disclosed. Stays a KPI overlay only (growth-rate commentary), never a modeled P&L line. |
| 28 | Will support revenue remain stable | A (partial) | Historical support (REV_330) is remarkably flat: $4,896M→$4,943M across 8 quarters (±1% band) — this is real empirical evidence of stability, usable as the base case's starting assumption; whether it *stays* stable through FY28 is still a forward judgment, scenario-differentiated. |
| 29 | Nonoperating investment value in equity value | A (partial) | Marketable securities (BS_020) are already a filed, extracted field ($605M FY26 Q4). Whether Oracle holds other nonoperating investments (e.g., residual equity stakes post-Ampere-sale) needs a targeted look at the FY26 10-K investments footnote before Gate 13's EV bridge — not a new document, a re-read. |
| 30 | Live institutional consensus for quarterly OCI/apps/margin/capex/EPS | B → Q-08 | Needs an authenticated data source (FactSet MCP connector exists but is unauthenticated) or user-provided terminal data. Not resolved here. |

**Summary:** 8 of 30 are genuinely closed to further research (2, 7, 9, 11 by
design; 17, 20, 22, 25/26/27 are inherently forward/market-dependent) — these
convert directly into scenario-differentiated assumption slots, not research
tasks. 10 are class A — a short list of footnote re-reads against documents
**already in the repo** (SRC-024) is worth doing before Gate 10 model build,
listed as action items in §7. 2 (Q-11, Q-08) need a specific new document/
connector, already tracked. The remainder are either fully resolved by
existing data (24, 28) or partially bounded by aggregate disclosures already
extracted (4, 13, 14, 16, 29).

## 3. Revenue driver architecture

Each stream keeps its Layer 3 field ID (REV_310–370); the forecast rule
replaces the historical population rule for FY27 Q1–FY28 Q4. No new field IDs.

### OCI (REV_310) — capacity/utilization model (Framework §2)

```
REV_310_t = ExistingCapacityIndex_t × Utilization_t × RevenuePerUnit_t
          + NewCapacityIndex_t × RampFactor_t × Utilization_t × RevenuePerUnit_t
```

Inputs and their status:
- `ExistingCapacityIndex`, `NewCapacityIndex` — **the Q-15 capacity contribution
  index**, defined and reconciled in §4 below (provisional, D-019).
- `Utilization`, `RampFactor`, `RevenuePerUnit` — no disclosed units exist
  (§2 items 7/8/9 above); these are **scenario-input multipliers calibrated to
  reproduce the historical REV_310 series exactly** at the FY26 Q4 jump-off
  point, then flexed by scenario per Framework §10's OCI growth ranges (not
  adopted here — Gate 8 input).
- Reconciliation checks at Gate 10: forecast REV_310 growth must cross-foot
  against (a) RPO conversion (RPO_020 × RPO_010, the "next-12-months" bucket)
  and (b) the DEBT_070 lease-commencement schedule — new capacity cannot
  generate revenue before its lease/CIP entry implies it is in service.

### Cloud applications (REV_320) — retention/expansion model

```
REV_320_t = REV_320_(t-4) × GrossRetention_t × Price/Expansion_t + NewGoLive_t
```
Real anchors: 8-quarter REV_320 history (flat ~$3.5-4.1B/qtr, ~11-13% YoY per
REV_135), Fusion/NetSuite growth-rate KPIs (KPI_010/020, growth-only per
architecture §5 — never used to impute dollar levels). `GrossRetention`,
`Price/Expansion`, `NewGoLive` are assumption slots calibrated to reproduce
historical growth, then scenario-flexed per Framework §10's applications-growth
ranges (Gate 8 input).

### Software support (REV_330) — renewal model

```
REV_330_t = OpeningSupportBase_t × RenewalRate_t × Price_t − Churn_t
```
Real anchor: the flattest series in the dataset (±1% across 8 quarters, §2
item 28) — base case should default to **near-zero net change**, a real
empirical finding, not an assumption dressed as one. Bear/bull cases flex
around a genuinely narrow historical band.

### Software licenses (REV_340) — pipeline/closing model

Framework explicitly instructs **not to smooth** this line. Real anchor: the
two-year, consistent Q4-concentration pattern (~39-40% of FY in Q4, §1). Driver
is qualitative (large-transaction pipeline, close rates) rather than a clean
formula; forecast should apply the empirical Q1-Q3 vs. Q4 split to an
assumed annual license total, not a quarterly growth rate.

### Hardware (REV_350) — units × ASP model

```
REV_350_t = Units_t × ASP_t
```
No unit/ASP disclosure exists; REV_350 is small (~4-5% of total revenue) and
structurally stable ($655M-$924M/qtr) — treat as a low-priority driver, held
near-flat with modest scenario flex, rather than building a full units×ASP
mechanism with no disclosed inputs to calibrate it.

### Services (REV_360) — headcount/utilization/billing-rate model

```
REV_360_t = BillableHeadcount_t × Utilization_t × BillingRate_t
```
No headcount/utilization/rate disclosure exists. Same treatment as hardware:
small stream (~7-8% of total), historically stable growth (~5-13% YoY implied
by REV_360 levels), forecast via a simple growth-rate assumption rather than a
three-factor model with no calibratable inputs.

### Bridge integrity (forecast quarters)

CHECK_020 (stream sum = REV_370 = total revenue) must hold in every forecast
quarter exactly as it does historically — this is a build-time control, not a
new decision.

## 4. Capacity contribution index (Q-15) — provisional definition, D-019

Framework §2 requires a capacity index because Oracle discloses no MW/GPU
units. Recommendation, offered in the same "analyst proposes, user ratifies"
pattern as D-014:

**Index construction:** `CapacityIndex_t = CapacityIndex_(t-1) + ΔNetPP&E_growth-attributable_t`,
rebased so **FY2026 Q4 = 100**. `ΔNetPP&E_growth-attributable` is approximated
by the quarterly increase in gross PP&E placed in service (BS_040 net level
plus the CIP-to-PP&E roll-off implied by BS_050) **net of the historical
non-AI-era PP&E base** (FY25 Q1 net PP&E of $23,094M, before the buildout,
serves as the pre-AI floor). This is deliberately a relative, unitless index —
never presented as MW or GPU count, which Oracle does not disclose (§2 item 7).

**Reconciliation requirement (per architecture's own instruction):** every
quarter, the index's implied capacity growth must be cross-checked against (a)
disclosed site/region additions (KPI_040, currently blank — populate as
disclosed), (b) the RPO commencement schedule (RPO_020's 12-month bucket and
RPO_050's duration buckets), and (c) the DEBT_070 lease-commencement window
(C-06: FY27-FY29). If the index and these three anchors diverge by more than a
qualitative sense-check, the index construction — not the anchors — is wrong
and must be revisited.

**Status:** provisional pending user sign-off, same status as D-014 before
ratification. Not required to block Gate 8 (scenario approval concerns the
*numeric ranges*, not this mechanical definition), but should be confirmed
before Gate 10 model build actually implements it.

## 5. Cost, margin, and depreciation mechanics

### Margin — top-down, not bottom-up (per §2 item 9 disposition)

No stream-level COGS or gross margin has ever been disclosed (COGS_310/320
stay structurally blank). Gross margin must be forecast **top-down** at the
consolidated level (COGS_050/060) using Framework §5's qualitative driver list
(utilization, power costs, depreciation, hardware ownership mix, contract
pricing, ramp inefficiency) as narrative justification for the chosen
consolidated margin path — never as a bottom-up build with fabricated
stream-level unit economics. Historical anchor: consolidated GAAP gross margin
declined from ~70.5% (FY25) to ~65.8% (FY26) as OCI mix grew (COGS_060 series
already in the reconciled file) — this trajectory, not stream-level guesses,
is the real starting point for FY27-28 scenario paths.

### Depreciation by vintage (PROF_140)

```
Depreciation_t = LegacyDepreciation_t + Σ_v [CapitalPlacedInService_v,t × DepreciationRate_v × DaysInService/365]
```
Vintage buckets keyed to CAP_040 (assets placed in service / PP&E roll-forward,
currently sparsely populated — needs the FY27 quarterly filings as they arrive)
and useful-life assumptions **pending the Note-4 footnote re-read** (§2 item
15). Historical depreciation (PROF_140) roughly doubled quarter-over-quarter
through FY26 ($1,351M Q1 → $2,415M Q4) as the PP&E base grew — this observed
acceleration is the real calibration target for the vintage model at the FY26
Q4 jump-off point.

### Operating expenses (OPEX_010-070)

No new mechanics needed — these are modeled as simple ratios-to-revenue or
absolute-dollar glide paths per line (S&M, R&D, G&A, SBC), calibrated to the
8-quarter historical actuals already in the reconciled dataset. Restructuring
(OPEX_060/065) is scenario-differentiated per Framework §2 item 25's
disposition (assumption).

## 6. Financing and dilution mechanics

### Debt roll-forward (DEBT_030)

```
EndingDebt_t = BeginningDebt_t + NewDebtIssuance_t + CapexFinancing_t − Repayments_t
Interest_t = AverageGrossDebt_t × EffectiveRate_t ÷ 4 + LeaseInterest_t + FinancingFees_t − CapitalizedInterest_t
```
`CapitalizedInterest_t` pending the §2 item 23 footnote check; if the FY26 10-K
does not disclose it, it is set to zero rather than assumed nonzero (matches
data-integrity hard rule — unknown = blank/zero-labeled, never invented).
Historical anchor for `EffectiveRate`: FY26 interest expense ($4.6B per the
Confirmed Consistencies note in `source_conflicts.md`) ÷ average FY26 gross
debt gives an empirical starting rate.

### Lease commencement (DEBT_050/060/070)

`DEBT_070` (currently $260B, C-06) rolls off into `DEBT_050/060` (on-balance-
sheet lease liabilities) on a schedule bounded by the FY27-FY29 commencement
window (§2 item 16) — no finer schedule is disclosed, so the within-window
distribution is a scenario input (front-/back-loaded bear-bull differentiation,
consistent with Framework §7's "power/construction delays" bear driver).

### Preferred security (DEBT_100/110) — pending Q-11

Both treatments from Framework §15 (debt-like vs. as-converted) are kept live
in the driver design; the switch is not thrown until Q-11 resolves (needs the
Certificate of Designations/prospectus). SHARE_060 (preferred conversion
effect) stays structurally forecast-only, consistent with architecture §16.

### ATM issuance / diluted shares (SHARE_010-070)

```
ATMSharesIssued_t = ATMProceeds_t ÷ AverageIssuancePrice_t
DilutedShares_t = BasicShares_t + RSUs/Options_t + ATMShares_t + PreferredConversionShares_t (if as-converted) + Other_t
```
`AverageIssuancePrice` is explicitly reflexive (Framework §5's "reflexive
dilution risk" — a weaker share price forces more shares issued for the same
proceeds) — this is the one driver where the **valuation output feeds back
into a forecast input**, and the model must handle it as an iterative or
scenario-fixed assumption, not a one-way calculation. Framework's illustrative
sensitivity ($110/$140/$180 issuance price → 181.8M/142.9M/111.1M shares from
a full $20B program) is a useful sense-check table, not an adopted assumption.

## 7. Action items before Gate 10 (targeted footnote re-reads, no new documents)

These use SRC-024 (already in the repo) and were not captured as dictionary
fields during Gates 4-6 because they weren't needed for the historical
reconciliation; they matter now for forecast mechanics:

1. PP&E useful-life ranges (Note 4) — for depreciation-by-vintage (§5, §2
   item 15).
2. Capitalized interest, if disclosed (debt/interest footnote) — §6, §2 item
   23.
3. BYOH capitalization/depreciation treatment language (Note 4) — §2 item 10.
4. Other nonoperating investments beyond marketable securities (investments
   footnote) — for the Gate 13 EV bridge, §2 item 29.

None of these block Gate 8 or Gate 9; they should be done as a short pass
before Gate 10's actual model build.

## 8. Scenario structure carried forward (not adopted — Gate 8 input)

Framework §9/§10's bear/base/bull operational differentiators (capacity
delivery timing, OCI margin band, applications growth band, financing mix,
credit trajectory) and its numeric ranges table are the **candidate starting
point** for Gate 8. They are reproduced in full in the Framework document
itself and are not re-transcribed here to avoid a second copy drifting out of
sync — Gate 8 must open the Framework §10 table directly, present it to the
user for explicit approval or adjustment (per CLAUDE.md's process-gate
requirement — "requires user sign-off + filled thesis doc"), and log the
ratified ranges as a new decision, the same way D-014 ratified the EBITDA
definition.

## 9. Valuation checkpoint scaffolding (structure only)

Four valuation dates and their NTM windows (Framework §14, Q-07):

| Valuation point | Expected timing | NTM forecast period |
|---|---|---|
| FY27 Q1 release | 2026-09-10 (management-scheduled) | FY27 Q2 – FY28 Q1 |
| FY27 Q2 release | est. December 2026 | FY27 Q3 – FY28 Q2 |
| FY27 Q3 release | est. March 2027 | FY27 Q4 – FY28 Q3 |
| FY27 Q4 release | est. June 2027 | FY28 Q1 – FY28 Q4 |

VAL_010-080 (already reserved in the data dictionary) populate at each date
per the walk-forward mechanic in Framework §14: replace the completed quarter
with actuals, reforecast the remaining seven quarters, recompute NTM, update
the debt/cash/lease/share stack, adjust the multiple for milestone achievement
(Framework §12), compute the new per-share target. The EV-to-equity formula
(Framework §15) is carried forward as-is; the lease-inclusion switch depends
on Q-13 (not resolved here) and the preferred-treatment switch on Q-11.

## 10. What remains open after Gate 7

Unchanged/still open: Q-04 (transcripts), Q-05 (analyst-day deck), Q-08
(consensus source), Q-11 (preferred treatment), Q-12 (NTM fiscal-alignment
convention), Q-13 (lease convention), Q-14 (peer weighting) — all Gate 8/9
scope, not Gate 7. Q-15's *definition* is issued provisionally (D-019) but its
ratification can happen alongside Gate 8 rather than blocking it. The §7
footnote re-reads are a short, non-blocking pre-Gate-10 task.

## 11. Next step (Gate 8)

Gate 8 requires the user to review and explicitly approve (or adjust) the
Framework §10 scenario ranges, using the now-completed user thesis document
(`ORCL_User_Thesis_and_Questions.docx`, D-018) as context for which direction
of adjustment (if any) matches the user's stated $150/multiple-expansion,
6-18 month, long-calls thesis. Gate 8 cannot be skipped or inferred — CLAUDE.md
marks it as requiring explicit sign-off.
