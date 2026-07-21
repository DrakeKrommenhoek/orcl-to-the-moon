# Gate 9 — Comparable-Company Methodology

Gate: 9 · Date: 2026-07-21 · Status: **ratified 2026-07-21 (D-021)** — user
approved §1-3 as proposed, no adjustments. §4 (multiple framework) remains an
unadopted Gate 13 candidate; §5 (C-09 market-data re-sourcing) remains
genuinely blocked, not a design decision.

Companions: `01_Research_Outputs/ORCL_Eight_Quarter_Model_Framework_2026-07-20.docx`
§6-8 (source of the peer table, valuation-method comparison, and multiple
framework), `00_project_control/source_conflicts.md` (C-09, C-10),
`00_project_control/open_questions.md` (Q-12, Q-14), `11_Analysis/forecast/
GATE7_FORECAST_DRIVER_DESIGN.md` (driver architecture this feeds into).

## 0. Scope boundary

Gate 9 decides *methodology*: which valuation method is primary, which peers
map to which Oracle business line, how much weight each peer carries, and how
NTM windows align across fiscal-year-end mismatches. It does **not** assign
scenario multiples with real numbers pulled from live market data (that needs
either FactSet authentication or user-supplied data, both currently
unavailable — Q-08), and it does not build the model (Gate 10+) or finalize
valuation (Gate 13).

## 1. Primary valuation methodology — recommendation

Adopt Framework §7's recommendation: **EV/NTM EBITDA with capital-adjusted
controls** as the primary method, cross-checked by five controls rather than
used in isolation:

1. Capex as a % of revenue
2. EBITDA less capex
3. Operating cash flow less capex
4. Lease-adjusted net leverage
5. Incremental ROIC

Rationale for primary method: EV/NTM EBITDA is neutral to Oracle's shifting
debt/equity mix, rolls forward cleanly at each of the four valuation dates,
and supports scenario-specific multiples (Gate 8's ratified bear/base/bull
cases plug directly into NTM EBITDA). Its stated weakness — EBITDA ignores
depreciation and the cash actually consumed building capacity, so it can make
an uneconomic capacity build look attractive — is exactly why the five
controls are mandatory alongside it, not optional cross-checks. A model that
reports EV/NTM EBITDA without also reporting EBITDA-less-capex and
lease-adjusted leverage at the same valuation date would misrepresent
Oracle's actual capital position; both should always be one glance apart in
the check tab and the output block.

Secondary/cross-check methods carried forward per Framework §7's own
comparison table (not adopted as primary, kept live as sanity checks):

| Method | Use here |
|---|---|
| P/NTM adjusted EPS | Direct per-share cross-check; captures interest, dilution, preferred — most sensitive to the still-open Q-11 preferred treatment |
| EV/NTM revenue | OCI-segment-only cross-check (SOTP), never for consolidated Oracle |
| Shadow sum-of-the-parts | Isolates OCI value; limited by disclosure (no segment profit reporting) — qualitative sense-check, not a primary number |
| DCF | Cross-check only; dominated by capex-normalization and terminal-value uncertainty per Framework's own caveat |

## 2. Peer set and weighting (Q-14)

Framework §6's business-line mapping, adopted as proposed:

| Oracle business | Primary comparables | Purpose |
|---|---|---|
| OCI | Microsoft, Amazon, Alphabet | Hyperscale infrastructure growth, margins, capex, capacity |
| Cloud applications | SAP, Salesforce | Enterprise SaaS growth, backlog, recurring margins |
| Support and licenses | IBM, SAP | Mature enterprise-software/support economics |
| Hardware and services | IBM + selected infrastructure vendors | Lower-growth product/service economics (no specific vendor list given by either research source — flag as a gap to fill at Gate 13 if a hardware-specific comp is needed; IBM alone is a thin proxy) |

Reference-only, never anchors (per Framework §6, adopted as-is): ServiceNow/
Workday (SaaS growth benchmark, materially less capital-intensive); Equinix/
Digital Realty (lease/data-center capital analysis only); Nvidia/AMD
(semiconductor economics); CoreWeave and other neoclouds (different financing/
customer-concentration risk — both AI research sources agree on this); pure-
SaaS median; broad mega-cap tech median; data-center REIT median.

**Q-14 resolution (recommendation):** the two AI research sources disagree in
*emphasis*, not in inclusion — Research Pack calls Amazon/Alphabet "weak
valuation comps," Framework calls them "primary OCI comparables." Neither
source argues to exclude them outright, and CoreWeave-as-reference-only is
already common ground (not in dispute). Resolve by **weighting within the OCI
peer group rather than treating it as a binary in/out call**:

- **Microsoft weighted heaviest** (~50%) within the OCI reference set — most
  comparable mixed profile (enterprise infrastructure + software + database +
  AI capex cadence), and per Framework §6 the closest analog for margin/capex
  trajectory.
- **Amazon and Alphabet weighted lower** (~25% each) — genuinely useful for
  hyperscale capex/margin/growth *cadence* benchmarking (which is what the
  Framework values them for) but diluted as a direct multiple anchor because
  retail/advertising dominate their consolidated financials (which is what the
  Research Pack's "weak comp" framing is really objecting to). Weighting
  down, not excluding, reconciles both sources' stated concerns without
  discarding either's valid point.
- This OCI-segment peer reference feeds into Framework §8's premium/discount
  bridge (`Oracle Multiple = Peer Reference + Growth Adj. + Margin Adj. −
  Capital Intensity − Leverage − Concentration − Execution Risk − FCF
  Penalty`) as a **starting reference point, not a mechanical average** — the
  bridge's own adjustment factors are where Oracle's capital-intensity and
  leverage differences from all three peers get priced in, so the weighting
  scheme does not need to solve that problem by itself.
- Applications peer group (SAP/Salesforce): weighted evenly, no disagreement
  between sources to resolve.
- CoreWeave: **confirmed reference-only** per both sources' agreement — never
  an anchor weight, used only as a pure-play AI-infrastructure multiple
  sanity-check.

## 3. NTM-window alignment convention (Q-12) — recommendation

Fiscal year ends in the peer set: Oracle 5/31; Microsoft 6/30 (near-aligned,
~1 month offset); Amazon/Alphabet/IBM/SAP 12/31 (5-month offset from Oracle);
Salesforce 1/31; ServiceNow 12/31.

**Recommendation:** build every NTM window (Oracle and peers alike) on a
**calendar-quarter basis** — the trailing four calendar quarters from each
valuation date — rather than "next four fiscal quarters as each company
defines them." A peer's own fiscal-quarter guidance/consensus is interpolated
onto calendar quarters (standard practice for comparing companies with
different fiscal calendars) before entering the comp multiple calculation.
Oracle's own fiscal-quarter forecast (FY27 Q1-FY28 Q4, the model's actual
driver output) is *not* restructured — the calendar conversion is a display/
comparison layer applied only when computing the comp multiple at each of the
four valuation dates, never a change to the underlying fiscal-quarter model.
This avoids the alternative failure mode (C-10): comparing Oracle's FY27 Q2
(Sep-Nov 2026) against, say, Amazon's own-labeled "next quarter" which might
be Oct-Dec 2026 — close but not the same period, and the gap compounds across
four quarters. Calendar-basis NTM removes the ambiguity for every comparison
in one convention rather than deciding it peer-by-peer.

## 4. Multiple framework — carried forward as a Gate 13 candidate, not adopted

Framework §8 proposes (self-labeled "analytical assumptions, not current
consensus or peer medians"):

| Scenario | EV/NTM EBITDA | P/NTM adjusted EPS |
|---|---|---|
| Bear | 9x-11x | 14x-16x |
| Base | 12x-14x | 18x-21x |
| Bull | 15x-17x | 23x-26x |

These are **not adopted here**. Gate 9 is methodology (which method, which
peers, which window convention); assigning the actual multiple numbers used
in the price-target calculation is Gate 13's job, and doing it properly needs
either live peer market data (blocked, Q-08/C-09 below) or an explicit
user-approved assumption set in the same style as D-020. Carried forward as
the candidate starting point, same treatment Gate 7 gave the scenario ranges
before Gate 8 ratified them.

## 5. C-09 status: comp market data is still unusable

C-09 already flags the existing comp table (prices, market caps, EV, NTM
estimates, multiples, as-of 2026-07-17/20) as single-sourced (Research Pack
only, citing TIKR/FactSet/S&P with no row-level attribution) and calls for
re-sourcing with explicit as-of dates before Gate 9/13. **That re-sourcing
cannot happen in this session:** the FactSet MCP connector in this workspace
is present but unauthenticated (Q-08), and no user-provided terminal data has
been supplied. Per the data-integrity hard rules, this project does not
substitute an LLM's general knowledge of current stock prices/multiples for a
properly sourced, as-of-dated figure — doing so would be exactly the kind of
unlabeled estimate C-03/C-08 already warn against for Oracle's own financials,
and the same standard applies to peer data. **This blocks nothing structural
in Gate 9** (the methodology above doesn't need live prices), but it fully
blocks Gate 13's actual multiple assignment and per-share output until one of:
(a) the user authorizes and the FactSet connector is authenticated, or (b) the
user supplies current peer market data with an as-of date.

## 6. Preferred-security interaction (Q-11, unresolved, cross-referenced only)

The P/NTM EPS cross-check method (§1) is the most exposed to Q-11's still-open
preferred-security treatment (debt-like vs. as-converted) — EPS moves
materially depending on which convention is used. Not resolved here; flagged
so Gate 13 doesn't discover the dependency late.

## 7. What remains open after Gate 9

Q-08 (consensus/live market-data source) and Q-11 (preferred treatment) both
still block quantitative work downstream (Gate 13's actual multiples and EPS
cross-check respectively). Q-04/Q-05 (transcripts/analyst day) remain open,
non-blocking. The hardware/services peer gap (§2) should be revisited at
Gate 13 if a more precise comp is needed.

## 8. Next step

Pending user confirmation of §1-3 (methodology, peer weighting, NTM
convention) — the same lightweight ratify-or-adjust pattern as prior gates.
Once confirmed, Gate 10 (minimal model build) can start using: the ratified
historical dataset (Gate 6), the driver architecture (Gate 7), the ratified
scenario ranges (Gate 8, D-020), and this gate's methodology — leaving actual
multiple assignment and per-share output for Gate 13 once Q-08/C-09 are
unblocked.
