# Decision Log

Decisions are numbered, dated, and never silently reversed — a reversal is a new entry.
Unresolved items belong in `open_questions.md`, not here.

## D-001 · 2026-07-20 · Adopt the checklist's numbered folder structure
The prior session's `00_MASTER_CHECKLIST.md` layout (`01_`–`09_` source folders) is
adopted as canonical rather than replaced, because it is intentional, logical, and the
downloaded filenames already match it. Extended with `00_project_control/` now and
reserved numbers `10_`–`13_` + `99_Archive/` for later gates. Empty folders are not
created in advance.

## D-002 · 2026-07-20 · Reorganization executed via git mv only
All file moves/renames per `PROPOSED_FILE_MOVE_MAP.md` were executed with `git mv`
(history-preserving, reversible). No source file content was modified. No files deleted.

## D-003 · 2026-07-20 · 10-K renames to checklist convention
`Oracle 2024 10K.pdf` and `Oracle 2025 10K.pdf` renamed to the checklist's exact target
names after verifying fiscal-year-end dates on page 1 of each PDF.

## D-004 · 2026-07-20 · AI research .docx files treated as the expected deep-research deliverables
The two root .docx files (Research Pack, Eight-Quarter Framework) are filed in
`01_Research_Outputs/` with dated ORCL-prefixed names, presumed to be the
ChatGPT/Gemini deliverables from the checklist (same 2026-07-20 date). Provider
attribution left open (Q-02). Both carry authority rank 6 regardless of provider.

## D-005 · 2026-07-20 · AI-report quarterly OCI/SaaS splits classified as estimates
Round-number quarterly OCI/SaaS revenue series in the Research Pack are classified as
research estimates, not disclosures (conflict C-03). The historical OCI/apps split will
be rebuilt from primary sources during extraction; where Oracle disclosure is
insufficient, the split will be labeled `calculated`/`assumed` with method notes.

## D-006 · 2026-07-20 · Source manifest is append-only and keyed by SRC-### IDs
Every future source file gets a manifest row on arrival; model inputs cite SRC IDs.

## D-007 · 2026-07-20 · Git strategy
Repository stays git-tracked including source PDFs (~50 MB total, stable, append-mostly).
`.gitignore` added for temp/derived/credential files. Git LFS deferred unless the repo
approaches ~1 GB or per-file 50 MB+ (Q-16). Work proceeds on branch
`claude/oracle-equity-model-mhmjq4`.

## D-008 · 2026-07-20 · Gate 1–3 (organizational portion) declared complete
Inventory, manifest, duplicate review (none found), and conflict register are done.
Numeric conflict *resolution* (C-01…C-11) is explicitly deferred to Gates 5–6.

## D-009 · 2026-07-20 · Three-layer historical architecture
Layer 1 = statements exactly as filed; Layer 2 = explicitly disclosed supplemental
metrics (release/slides/MD&A/footnotes) at disclosed precision; Layer 3 = six-stream
analytical architecture populated historically only through the documented bridge in
`HISTORICAL_DATA_ARCHITECTURE.md` §7. AI-report estimates can satisfy no layer.

## D-010 · 2026-07-20 · YTD cash-flow handling fixed
10-Q cash-flow figures stored as-filed (YTD) in dedicated fields; standalone quarters
exist only as calculated fields via Q1=YTD1, Q2=YTD2−YTD1, Q3=YTD3−YTD2, Q4=FY−YTD3,
with the validation battery in `HISTORICAL_RECONCILIATION_PLAN.md` §15.

## D-011 · 2026-07-20 · Blank-beats-guess extraction rule
Where rungs 1–6 of the precedence ladder disclose nothing, the historical cell stays
blank with status `not_disclosed`. Rounded disclosures keep stated precision. AI research
reports are barred from supplying any historical financial value (implements C-03/C-04/
C-08; extends D-005).

## D-012 · 2026-07-20 · Stable field-ID interface
132 fields across 13 families (REV_, COGS_, OPEX_, PROF_, CF_, BS_, DEBT_, SHARE_, KPI_,
RPO_, CAP_, VAL_, CHECK_) in `orcl_data_dictionary.csv`. Field IDs are permanent; scripts
and spreadsheets reference IDs, never labels. ID gaps (10s) allow insertion without
renumbering.

## D-013 · 2026-07-20 · Dual-presentation Layer 1 for the FY26 reclassification (Q-18)
Oracle's FY26 filings reclassify the filed income statement (Cloud/Software captions,
"Cloud and software" expense relabel, 10-K-level "Restructuring and other" merge,
preferred-dividend EPS mechanics). Rather than redefining existing fields, five fields
were added — REV_011 (Cloud, as filed FY26), REV_021 (Software, as filed FY26),
REV_147 (Software license, by offerings), COGS_011 (Cloud and software expenses),
OPEX_065 (Restructuring and other, combined caption) — and the Layer 3 bridge was
amended for FY26-presentation periods: REV_330 = REV_145 (software support is now
directly disclosed, no residual), REV_340 = REV_147. Pre-FY26 fields (REV_010/020,
COGS_010, REV_140) stay defined as-was and are `not_disclosed` from FY26 Q1. Each
period is stored exactly as filed; the recast comparatives in FY26 filings are the
documented bridge (they tie exactly). Field IDs remain stable; no extracted value was
ever redefined. Dictionary/mapping updated to 137 rows; template regeneration deferred
to Gate 5B start (original Gate 4 template preserved unchanged).

## D-014 · 2026-07-20 (ratified 2026-07-21) · EBITDA definition (Q-10)
Primary historical EBITDA (PROF_160) = GAAP operating income (PROF_010) + cash-flow-
statement depreciation (PROF_140) + amortization of intangibles (CF basis). SBC is NOT
added back; restructuring/acquisition costs stay in (a separate "adjusted EBITDA"
series may add them back at Gate 13); operating-lease expense stays in (EBITDA, not
EBITDAR — consistent with borrowings-only gross debt per C-01); one-time investment
gains (Ampere, Bloom) are excluded by construction because they sit below operating
income. Cross-check series: non-GAAP operating income + depreciation. FY26 values:
primary 29,900; NI-up variant 33,447; non-GAAP variant 36,549 — materially different,
never interchangeable. Full memo: 11_Analysis/historical/EBITDA_DEFINITION_MEMO.md.
**User signed off 2026-07-21 on definition 1 as recommended, no adjustments.**
PROF_160 values across all quarters/annuals relabeled `ratified 2026-07-21 per user
sign-off`. Q-10 closed.

## D-015 · 2026-07-20 · Q4 value precedence and pilot provenance format
(a) Where the Q4 release directly discloses a standalone Q4 statement line, the release
value is stored as `reported` and the FY-minus-9M derivation is the validation (five
lines differ by exactly $1M due to recast rounding — documented, within tolerance).
Where no direct Q4 disclosure exists (cash flows, depreciation, interest income,
by-offerings sub-streams), the FY−9M value is stored as `calculated` with both source
citations. Derivations are refused where FY and 9M captions are inconsistent (CF_040
acquisitions; CP vs short-term-financing split) — those cells are `not_disclosed`.
(b) The template-shaped extraction file cannot carry per-cell provenance, so the pilot
introduces a companion long-format file (`orcl_historical_quarterly_pilot_provenance.csv`,
one row per populated value with source ID/filename/section/classification/GAAP-tag/
formula/precision/status/notes). This two-file pattern is the standard for Gate 5B.

## D-016 · 2026-07-20 · Gate 5B disclosure-evolution findings (lease footnote + IaaS/SaaS precision)
Two independent Oracle disclosure-architecture changes were confirmed during full
extraction, distinct from the Q-18 statement-caption reclassification (D-013):
(a) the dedicated lease supplemental-balance-sheet footnote (ROU assets,
current/non-current liability split) does not exist in the FY2025 Q1-Q3 10-Qs —
first appears at FY2025 Q4/annual (10-K) and becomes a standard quarterly footnote
from FY2026 Q1 onward. BS_060/DEBT_050/DEBT_060 are therefore genuinely
`not_disclosed` for FY2025 Q1-Q3, not an extraction gap; (b) exact-millions IaaS/SaaS
quarterly dollars (REV_120/REV_130) for FY2025 were never disclosed in their own
period's release (headline billions only) but were later published as recast
comparatives in the FY2026 Q1 and Q4 releases (SRC-013/SRC-016). Per the precedence
rules, a later official Oracle release remains rung 3 regardless of which period it
covers, so these comparative figures were adopted as the primary FY2025 REV_120/130
values (precision upgrade), with both the original headline disclosure and the
later exact-millions source cited in every affected row. Dictionary notes and the
disclosure matrix updated accordingly; no field IDs changed.

## D-017 · 2026-07-20 · Gate 5B extraction file naming (full extraction supersedes pilot for modeling)
The Gate 5A pilot files (`orcl_historical_quarterly_pilot.csv` and its provenance)
are retained unmodified as the audit record of the two-quarter proof-of-concept.
Gate 5B's full eight-quarter extraction lives in new files
(`orcl_historical_quarterly_full.csv` / `_full_provenance.csv`) built from a
superset script that reuses the pilot's FY2026 Q1/Q4/annual entries verbatim
(no re-transcription, no value drift) and adds FY2025 Q1-Q4 + FY2026 Q2-Q3. The
full file is the one to use for Gate 6 reconciliation and Gate 7+ forecasting.

## D-018 · 2026-07-21 · User thesis captured (Q-06)
`01_Research_Outputs/ORCL_User_Thesis_and_Questions.docx` was filled in via
clarifying questions rather than left for the user to draft freeform, since Gate 8
(scenario approval) needs it and the user asked to be asked. Captured: interest
driven by OCI/cloud-infrastructure growth, the multi-cloud database moat (Autonomous
Database, Fusion/NetSuite stickiness), and a valuation/mean-reversion view (fair
value seen as significantly above the current price); 6–18 month holding period;
instrument is long calls, max acceptable downside is full premium; year-end price
narrative is multiple expansion to $150, expected within 2–3 quarters if not by EOY
2026; invalidation triggers are balance-sheet/leverage stress, an AI capex bust, and
margin compression from the depreciation buildout outpacing revenue. The four
earnings dates use Q-07's canonical set (FY27 Q1 2026-09-10, management-scheduled;
Q2/Q3/Q4 are estimates per historical release-timing patterns, to be confirmed
against Oracle's IR calendar closer to each date). Q-06 closed; Gate 8 no longer
blocked on the thesis doc (Q-11 and the remaining Gate 6 blockers are unrelated and
still open).

## D-019 · 2026-07-21 · Capacity contribution index definition (provisional, Q-15)
Recommended (Gate 7): `CapacityIndex_t = CapacityIndex_(t-1) + ΔNetPP&E growth
attributable to the buildout`, rebased so FY2026 Q4 = 100. Deliberately a
relative, unitless index — Oracle discloses no MW/GPU/equivalent capacity unit
(architecture §19), so no absolute-unit index is constructible from filings.
Reconciliation requirement: cross-check implied capacity growth each quarter
against disclosed site/region additions (KPI_040), the RPO next-12-months and
duration buckets (RPO_020/050), and the DEBT_070 lease-commencement window
(FY2027-FY2029 per C-06). Full rationale: `11_Analysis/forecast/
GATE7_FORECAST_DRIVER_DESIGN.md` §4. Provisional in the same pattern as D-014
before its ratification — does not block Gate 8, should be confirmed before
Gate 10 implements it.

## D-020 · 2026-07-21 · Scenario ratification (Gate 8)
User reviewed the Framework §9/§10 bear/base/bull operating-scenario
definitions and numeric ranges (reproduced in `GATE_7_REVIEW.md`'s Gate 8
handoff and presented in full in this session) and **approved them as
proposed, no adjustments**, including confirming the Bear case's severity
(OCI gross margin <30%, more debt/ATM dilution at a depressed price, deeply
negative FCF, worsening credit metrics) is an adequate representation of the
user's stated invalidation triggers (balance-sheet/leverage stress, an AI
capex bust, margin compression — D-018). Ratified scenario set:

| Driver | Bear (FY27/FY28) | Base (FY27/FY28) | Bull (FY27/FY28) |
|---|---|---|---|
| OCI growth | 88-98% / 50-65% | 112-118% / 85-100% | 130-140% / 95-115% |
| Applications growth | 7-9% / 6-8% | 10-12% / 10-12% | 14-16% / 13-15% |
| Total revenue | $84-86B / $108-116B | $89.5-90.5B / $127-132B | $94-97B / $140-150B |
| GAAP gross margin | 53-56% / 50-54% | 55-58% / 52-57% | 58-60% / 57-61% |
| Non-GAAP op margin | 36-38.5% / 34-38% | 39.5-41.5% / 38.5-41.5% | 42-44% / 42-45% |
| Gross capex | $92-100B / $85-105B | $90-95B / $100-115B | $95-105B / $115-135B |
| FY27 net cash capex | $75-82B | $68-72B | $65-75B |
| Depreciation | $13-15B / $23-29B | $15-17B / $28-34B | $17-20B / $32-40B |
| Interest expense | $7.0-8.0B / $8.0-9.5B | $6.0-7.0B / $7.0-8.5B | $5.5-6.5B / $6.0-7.5B |
| Ending gross debt | $155-165B / $175-195B | $145-153B / $155-175B | $138-148B / $140-160B |
| Ending cash | $12-20B / $10-18B | $20-28B / $18-28B | $28-38B / $30-45B |
| Diluted shares | 3.10-3.17B / 3.18-3.28B | 3.03-3.10B / 3.11-3.20B | 2.98-3.06B / 3.04-3.13B |

These ranges are now the model's ratified operating-scenario inputs for Gate
10 build (subject to the driver *mechanics* designed at Gate 7, and to D-019's
capacity-index definition once separately confirmed). The multiple/valuation
assumption that translates an operating case into the user's $150 price
target is a distinct Gate 9/13 decision, not resolved by this ratification.
Gate 8 closed.

## D-021 · 2026-07-21 · Comps methodology (Gate 9)
User reviewed and approved as proposed, no adjustments, all three
recommendations in `11_Analysis/valuation/GATE9_COMPS_METHODOLOGY.md`:
(1) **Primary valuation method:** EV/NTM EBITDA with five mandatory controls
(capex/revenue, EBITDA-less-capex, OCF-less-capex, lease-adjusted net
leverage, incremental ROIC) — never reported without the controls alongside
it. Cross-checks: P/NTM adjusted EPS, EV/NTM revenue (OCI-segment only),
shadow SOTP, DCF.
(2) **Peer set and weighting (Q-14 resolved):** OCI → Microsoft (~50%
weight)/Amazon (~25%)/Alphabet (~25%) — the two AI research sources' Amazon/
Alphabet disagreement is resolved by weighting down rather than excluding,
since both sources agreed on inclusion and disagreed only on emphasis;
Applications → SAP/Salesforce (even weight); Support/license → IBM/SAP;
Hardware/services → IBM (thin proxy, flagged gap). CoreWeave confirmed
reference-only per both sources. ServiceNow/Workday, Equinix/Digital Realty,
Nvidia/AMD, pure-SaaS/mega-cap-tech/data-center-REIT medians: reference-only,
never anchors.
(3) **NTM-window alignment (Q-12 resolved):** every company's NTM window
built on a calendar-quarter basis (peer fiscal-quarter data interpolated onto
calendar quarters), not "next four fiscal quarters" as each company defines
them — avoids comparing economically mismatched periods across Oracle's 5/31
FYE and peers' 6/30/12/31/1/31 FYEs (C-10).
Explicitly NOT adopted: the Framework §8 multiple ranges (EV/NTM EBITDA
9-11x/12-14x/15-17x bear/base/bull) — carried forward as a Gate 13 candidate
only, since real multiple assignment needs live peer market data, which
remains blocked (C-09/Q-08: FactSet connector unauthenticated, no user-
supplied terminal data). Q-11 (preferred treatment) flagged as a live
dependency for the P/NTM EPS cross-check, not resolved here. Gate 9 closed.

## D-022 · 2026-07-21 · Gate 10 minimal model build
Built `12_Model/development/ORCL_8Q_Model_v0.1_Gate10.xlsx`: Control Panel
(scenario + valuation-date switches), Historical Actuals (Gate 6 dataset),
Scenario Assumptions (full D-020 table with a Selected-scenario midpoint
column), Revenue Forecast (six streams, FY27 Q1-FY28 Q4, OCI/applications
growth scenario-switched per D-020, the other four streams held at trailing
FY26 actual growth pending a ratified range for them), Margin & EBITDA
(top-down per Gate 7 §5, EBITDA per the ratified D-014 definition), and
Checks (stream-additivity and quarter-to-FY ties, historical and forecast).
**Environment note:** LibreOffice's headless recalculation is broken in this
sandbox (confirmed via isolated tests — even a trivial one-formula workbook
hangs indefinitely on the same step, independent of this workbook's content).
Verified instead by (a) a zero-count programmatic check for unquoted
multi-word cross-sheet references, and (b) an independent Python replica of
the Base-scenario formula chain, which lands the bottom-up revenue build at
FY27 $90.5B / FY28 $129.1B — inside the Framework's own top-down base-case
ranges without being forced to match them. Full detail: `GATE_10_REVIEW.md`.
Not built (Gate 12 scope): debt/lease/ATM mechanics, depreciation-by-vintage,
diluted shares, valuation output. One documented gap: GAAP operating margin
has no ratified scenario range, held flat at the FY26 actual pending Gate 12.

## D-023 · 2026-07-21 · Gate 11 model checks
Added CHECK_090 (GAAP/non-GAAP operating income bridge) to
`ORCL_8Q_Model_v0.2_Gate11.xlsx`, historical quarters only: re-derives
`Non-GAAP operating income − GAAP operating income` from the individually
filed reconciling items (OPEX_040 amortization, OPEX_070 SBC, combined
acquisition-related/restructuring using OPEX_065's FY26-Q4 combined caption)
and compares against the as-extracted PROF_030 — a genuine second-source
check, not a tautology. Ties within $1mm rounding across all 8 historical
quarters, verified independently in Python both before and after wiring the
formulas into the workbook. Re-attempted LibreOffice headless recalculation
with a 290s budget — still hangs, confirming Gate 10's finding is a
persistent sandbox limitation, not a one-off. v0.1 archived unchanged to
`12_Model/archived_versions/` before this session's edits, per CLAUDE.md's
model-versioning rule. Balance-sheet/cash-flow ties correctly deferred to
Gate 12, since those schedules don't exist yet. Full detail:
`GATE_11_REVIEW.md`.

## D-024 · 2026-07-21 · Gate 12 full model build
Added four tabs to `ORCL_8Q_Model_v0.3_Gate12.xlsx` (v0.2 archived first):
Capex & Depreciation (splits depreciation from amortization of intangibles
for the first time — Margin & EBITDA's D&A line re-linked to this split
build, replacing Gate 10's combined envelope); Debt, Leases & Cash (debt
roll-forward from the FY26 Q4 actual to D-020's scenario-selected ending
debt, net issuance as an explicit plug since no issuance schedule is
disclosed; lease-commencement schedule spreading the disclosed $260B
uncommenced-lease pool evenly across the FY2027-FY2029 window per the FY26
10-K, C-06; ending cash on the same scenario-endpoint-plus-plug pattern);
Equity & Shares (diluted shares pull D-020's scenario-selected figure
directly, not re-derived from an assumed reflexive ATM price); Cash Flow &
Returns (implied operating cash flow solved as a cash-identity plug, four of
D-021's five mandated EV/NTM-EBITDA controls — capex/revenue, EBITDA-less-
capex, OCF-less-capex/FCF, lease-adjusted net leverage; incremental ROIC
explicitly not built, deferred to Gate 13). Checks tab gained CHECK_080
(debt roll-forward) and CHECK_100 (cash tie), both labeled as true-by-
construction identities rather than independent validations. Verified via a
full-chain Python replica of the Base scenario (FY27 EBITDA ~$45.1B/FCF
~-$26.7B/leverage ~5.4x; FY28 EBITDA ~$71.8B/FCF ~-$17.0B/leverage ~4.8x,
improving as the Framework's own base case narrative expects) and a repeated
zero-count check for unquoted cross-sheet references. Full detail:
`GATE_12_REVIEW.md`.

## D-025 · 2026-07-21 · Gate 13 valuation — buildable portion
Added a Net Income & EPS bridge (interest expense → pre-tax income → tax at
a held-flat trailing FY26 effective rate of 12.6% → net income → less
preferred dividends → ÷ diluted shares → GAAP EPS) to Margin & EBITDA, and a
new "Valuation (Gate 13)" tab to `ORCL_8Q_Model_v0.4_Gate13.xlsx` (v0.3
archived first): NTM revenue/EBITDA/EPS aggregation at exactly the four
Framework-specified valuation dates; the enterprise-to-equity bridge
(gross debt, on-balance lease liabilities, preferred, cash + marketable
securities) pulled at each valuation date's just-completed quarter, with
Q-11 (preferred debt-like default) and Q-13 (leases included) flagged as
unresolved rather than silently assumed settled. **Real multiple assignment
left genuinely blank (yellow-highlighted cells)** — this is Gate 13's one
external blocker, not a design choice: Q-08 (FactSet unauthenticated) and
C-09 (existing comp table stale/single-sourced) mean no real, as-of-dated
EV/NTM EBITDA or P/NTM EPS multiple can be sourced this session, and filling
it from general knowledge would violate the no-fabricated-data rule. An
explicitly-labeled illustrative-only section demonstrates the mechanism
using the Framework's own unadopted 12x-14x base-case candidate (midpoint
13.0x), producing $165.57/share at the first valuation date — coincidentally
near the user's own $150 thesis target, a useful sanity signal that the
mechanism isn't broken, never to be quoted as a real price target. Verified
via a full-chain Python replica matching the actual formulas cell-by-cell.
Full detail: `GATE_13_REVIEW.md`.

## D-026 · 2026-07-21 · Gate 14 sensitivities — illustrative bear/base/bull range
Added a "Sensitivities (Gate 14)" tab to `ORCL_8Q_Model_v0.5_Gate14.xlsx`
(v0.4 archived first): Bear/Bull NTM revenue and D&A computed directly from
the Scenario Assumptions Bear/Bull columns (the Control Panel switch only
drives one case at a time, so this bypasses it for a genuine three-case
comparison); bridge components (debt/cash/shares) pulling each scenario's own
D-020 ending range; and — per the user's explicit instruction to proceed
with the illustrative multiple — the actual bear/base/bull illustrative
price triad at the FY27 Q1 valuation date: **Bear ~$96/share (10.0x), Base
~$166/share (13.0x), Bull ~$244/share (16.0x)**, correctly ordered bear <
base < bull. Also added a one-way sensitivity table (Base NTM EBITDA held
fixed, multiple varied 9x-17x). Same illustrative-only labeling as Gate 13
throughout — Q-08/C-09 remain unresolved, so no real multiple exists yet.
Scope explicitly limited to the first valuation date via a closed-form
approximation, not a full quadrupled quarterly Bear/Bull rebuild across all
four dates (documented as a reasonable future refinement, not a gap in this
gate's deliverable). Verified via an independent Python replica matching the
actual formulas, both individually and via the monotonic bear<base<bull
ordering as a sanity check. Full detail: `GATE_14_REVIEW.md`.

## D-027 · 2026-07-21 · Gate 15 investment interpretation memo
Published `13_Deliverables/GATE15_INVESTMENT_INTERPRETATION_MEMO.md`,
checking the ratified user thesis (D-018: long calls, 6-18 month hold,
full-premium downside tolerance, $150 target via multiple expansion) against
the Gate 14 illustrative bear/base/bull triad (~$96/$166/$244). Findings:
the $150 target sits between illustrative Base and Bull, a coherent reading
of "multiple expansion," not a contradiction; long calls remain the right
structural fit given the user's own risk tolerance and holding period (a
call spread would cap upside the thesis doesn't ask to cap); the user's
three invalidation triggers map directly onto the ratified Bear case's
defining features and the D-021 controls — the project's risk framework and
the user's personal one are the same thing. Strike/expiration explicitly
left undecided — needs real current option prices/IV, not fabricated.
Before this memo, issued a structured research prompt
(`11_Analysis/valuation/RESEARCH_PROMPT_FOR_EXTERNAL_AI.md`) for the user to
run through Gemini/ChatGPT/Perplexity, targeting Q-08/C-09 (real multiple),
Q-11 (preferred terms), and Q-04/Q-05 (transcripts/analyst day) — framed as
rank-6 research-tool output per the source hierarchy, usable only with a
named source and as-of date. All fifteen CLAUDE.md process gates have now
been touched; remaining work is data acquisition, not further design or
construction. Full detail: `GATE_15_REVIEW.md`.

## D-028 · 2026-07-22 · Research prompt results processed; Q-11 substantively resolved
User ran the Gate-15 research prompt through both Gemini Deep Research and
ChatGPT; both outputs saved as new sources (SRC-025, SRC-026, rank 6 —
research-tool output, cross-check only per the source hierarchy). Key
findings, cross-corroborated between the two independently-run tools
(precise numeric agreement on the preferred terms is a meaningful confidence
signal even though neither citation was independently fetched by this
session — SEC.gov returned 403 to a direct WebFetch attempt):
- **Q-11 substantively resolved.** Series D mandatory convertible preferred:
  minimum/maximum conversion rates 499.8126/624.7657 common shares per
  preferred share, initial price ~$160.06, threshold appreciation price
  ~$200.07, mandatory conversion date **~2029-01-15**. Since
  every one of this project's four valuation dates falls in 2026-2027, well
  before mandatory conversion, **debt-like treatment is structurally
  correct for all four dates**, not a default pending resolution — this is
  what Gates 12-14 already did, now confirmed rather than assumed.
- **Q-08 remains open but partially informed.** Peer EV/NTM EBITDA multiples
  disagree materially between the two tools (C-12) — not usable as "the"
  real multiple. Oracle's own current market-implied EV/NTM EBITDA (13.76x,
  Gemini) is a single-entity ratio not exposed to the same peer-methodology
  mismatch, and lands almost exactly on the illustrative Base case's 13.0x
  used since Gate 9 — a real-world cross-check, not a full resolution of
  Q-08, added to the Valuation (Gate 13) tab as a separate labeled line.
- **Q-04/Q-05 partially informed**, not fully resolved: substantive
  transcript-backed commentary now available (97.5% GPU utilization, BYOH
  contract mechanics, steady-state ROIC "high 20s", partner-funded capacity,
  32% OCI gross margin on delivered capacity) but not independently verified
  against the actual transcripts (still not obtained, Q-04). FY2030 OCI
  target disagrees between tools ($100-120B vs. $166B, C-13) — unresolved,
  not used in the model.
- Current ORCL price/market cap (~$126, ~$360-366B), FY27 revenue guidance
  (~$90B) and non-GAAP EPS guidance ($8.05), and FY2030 analyst-day targets
  ($225B revenue, $21.00 EPS) all cross-corroborate cleanly between the two
  tools and against figures already in the repo.
Full detail and the resulting model/memo updates: see the Gate 13/15 model
and memo updates made this session, and `source_conflicts.md` C-12/C-13.
