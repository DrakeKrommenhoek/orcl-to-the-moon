# CURRENT_STATE

Last updated: 2026-07-21 (Gate 14 sensitivities session — illustrative multiple)
Branch: `claude/oracle-historical-extraction-handoff-7dn6cr` (remote =
DrakeKrommenhoek/orcl-to-the-moon). Rebuilt 2026-07-21 on top of
`claude/oracle-historical-extraction-pilot-r6o3ov`, which carries the actual
Gate 5A/5B/6 work — the originally assigned handoff branch had been deleted
upstream with no PR ever opened, so this session restarted it from the branch
that actually held the completed work.

## Current phase

**Gate 14 (sensitivities) COMPLETE, on the illustrative multiple** — per
explicit user instruction. Gate 13 (valuation) remains partially complete:
NTM aggregation, the enterprise-to-equity bridge, and Net Income/EPS
mechanics are built; real multiple assignment is still genuinely blocked on
Q-08/C-09 (no authenticated market-data source). Gates 1-12 complete (see
below). **Next: Gate 15 (investment interpretation), or resolve Q-08 first
to redo Gates 13-14 with a real multiple.**

## Completed work

- Gates 1-3: inventory, manifest (24 sources), duplicate review, conflict register.
- Gate 4: three-layer architecture, data dictionary, mapping, matrix, template,
  reconciliation plan, precedence rules.
- **Gate 5A (pilot):** FY2026 Q1 + Q4 proof-of-concept. See `GATE_5A_PILOT_REVIEW.md`.
- **Gate 5B:** full eight-quarter extraction (FY2025 Q1 - FY2026 Q4 + both
  annuals) - 839 values, 96 not-disclosed. See `GATE_5B_REVIEW.md`.
- **Gate 6:** historical reconciliation - 140 checks (136 pass / 4 blocked / 0
  fail), C-01/C-02/C-06/C-07 all resolved. See `GATE_6_REVIEW.md`.
- **D-014 (EBITDA definition) ratified 2026-07-21** — user approved the
  recommended definition (GAAP operating income + CF depreciation +
  amortization of intangibles, no SBC add-back) as proposed, no adjustments.
  PROF_160 relabeled ratified across all periods. Q-10 closed.
- **Q-06 (user thesis) resolved 2026-07-21 (D-018)** — thesis captured via
  clarifying questions and written into `ORCL_User_Thesis_and_Questions.docx`:
  OCI growth/database moat/mean-reversion thesis, 6-18 month hold, long calls
  (max downside = full premium), $150 year-end target via multiple expansion
  within 2-3 quarters if not by EOY 2026, invalidation = leverage stress/AI
  capex bust/margin compression. Gate 8 no longer blocked on this doc (though
  Gate 8 itself still needs explicit user sign-off on the scenario ranges).
- **Gate 7 (this session): forecast-driver design.** See `GATE_7_REVIEW.md`
  and the full deliverable `11_Analysis/forecast/GATE7_FORECAST_DRIVER_DESIGN.md`.
  - Empirical seasonality computed from the Gate 6 reconciled history for all
    six revenue streams (both fiscal years).
  - All 30 Framework §16 unresolved questions triaged: 8 permanently
    assumption/scenario-input by design, 10 partially answerable from
    documents already in the repo (short pre-Gate-10 footnote-recheck list,
    not new document requests), 2 needing a tracked new document/connector
    (Q-11, Q-08), rest resolved/bounded by existing data.
  - Explicit forecast driver formula designed for each of the six revenue
    streams, cost/margin architecture (top-down, since no stream-level margin
    is ever disclosed), depreciation-by-vintage, debt/lease/ATM/preferred
    mechanics (with the reflexive ATM-price-vs-valuation loop flagged
    explicitly), and valuation-checkpoint scaffolding.
  - **D-019 (provisional):** capacity contribution index (Q-15) definition
    recommended — relative, unitless, rebased to FY26 Q4 = 100. Same
    provisional-pending-sign-off pattern D-014 was in; does not block Gate 8.
  - No new field IDs introduced — forecast quarters populate the existing
    field set under `historical_or_forecast = forecast`.
- **Gate 8 (this session): scenario approval.** See `GATE_8_REVIEW.md` and
  **D-020** in `decision_log.md`. Presented the Framework §9/§10 bear/base/bull
  operating-scenario definitions and full numeric-range table (FY27/FY28,
  twelve driver rows) to the user against the ratified thesis (D-018). **User
  approved as proposed, no adjustments**, including confirming the Bear case's
  severity adequately represents their leverage-stress/AI-capex-bust/margin-
  compression invalidation triggers. D-020 is now the single source of truth
  for the ratified ranges — Gate 10 build reads from there, not the Framework
  docx. The multiple/valuation assumption that turns an operating case into a
  per-share price is explicitly deferred to Gate 9/13, not resolved here.
- **Gate 9 (this session): comps methodology.** See `GATE_9_REVIEW.md` and
  **D-021** in `decision_log.md`. Ratified: (1) primary valuation method =
  EV/NTM EBITDA with five mandatory capital-adjusted controls; (2) peer set/
  weighting (Q-14 resolved) — Microsoft ~50%/Amazon ~25%/Alphabet ~25% within
  the OCI reference, resolving the two AI research sources' disagreement by
  weighting rather than exclusion; CoreWeave confirmed reference-only; (3)
  NTM-window alignment (Q-12 resolved) — calendar-quarter basis for every
  company. **Not adopted:** the Framework's multiple ranges (9-11x/12-14x/
  15-17x EV/EBITDA) — carried forward as a Gate 13 candidate only, since real
  multiple assignment needs live peer market data, still blocked by Q-08/C-09
  (FactSet unauthenticated, no user-supplied terminal data) — flagged, not
  fabricated.
- **Gate 10 (this session): minimal model build.** See `GATE_10_REVIEW.md` and
  **D-022** in `decision_log.md`. Built
  `12_Model/development/ORCL_8Q_Model_v0.1_Gate10.xlsx` — six tabs (Control
  Panel, Historical Actuals, Scenario Assumptions, Revenue Forecast, Margin &
  EBITDA, Checks). One scenario switch (Control Panel dropdown) drives the
  D-020 ratified ranges through the whole workbook via a Selected-scenario
  column. Revenue forecast is scenario-switched for OCI/applications growth;
  the other four streams are held at trailing FY26 actual growth pending a
  ratified range for them. EBITDA follows the ratified D-014 definition.
  **Environment note:** LibreOffice's headless recalculation is broken in
  this sandbox (confirmed via isolated tests unrelated to this workbook's
  content) — verified instead via a zero-count check for unquoted cross-sheet
  references and an independent Python replica of the Base-scenario formula
  chain, which lands the bottom-up build at FY27 $90.5B / FY28 $129.1B,
  inside the Framework's own base-case ranges without being forced to match.
  Not built (Gate 12 scope): debt/lease/ATM mechanics, depreciation-by-
  vintage, diluted shares, valuation output.
- **Gate 11 (this session): model checks.** See `GATE_11_REVIEW.md` and
  **D-023** in `decision_log.md`. Added CHECK_090 (GAAP/non-GAAP operating
  income bridge) to `12_Model/development/ORCL_8Q_Model_v0.2_Gate11.xlsx`,
  historical quarters only — re-derives non-GAAP operating income from the
  individually filed reconciling items (SBC, amortization, acquisition-
  related/restructuring) and compares against the as-extracted figure. A
  genuine second-source check: ties within $1mm rounding across all 8
  quarters. v0.1 archived to `12_Model/archived_versions/` before edits.
  Re-attempted LibreOffice recalculation (290s budget) — still hangs,
  confirming Gate 10's finding is persistent, not a one-off. Balance-sheet/
  cash-flow checks correctly deferred to Gate 12 (schedules don't exist yet).
- **Gate 12 (this session): full model build.** See `GATE_12_REVIEW.md` and
  **D-024** in `decision_log.md`. Added four tabs to
  `12_Model/development/ORCL_8Q_Model_v0.3_Gate12.xlsx` (v0.2 archived
  first): Capex & Depreciation (splits depreciation from amortization for the
  first time; re-linked Margin & EBITDA's D&A line to it); Debt, Leases &
  Cash (debt roll-forward and lease-commencement schedule off the FY26 Q4
  actual and D-020's scenario-selected endpoints, net issuance/OCF as
  explicit plugs since no issuance schedule is disclosed); Equity & Shares
  (diluted shares pull D-020 directly, not re-derived from a circular ATM-
  price assumption); Cash Flow & Returns (four of D-021's five mandated
  valuation controls — ROIC explicitly not built, deferred to Gate 13).
  Checks tab gained CHECK_080/CHECK_100 (debt/cash ties, true by
  construction). Verified via a full-chain Python replica of the Base
  scenario (FY27 EBITDA ~$45.1B/FCF ~-$26.7B/leverage ~5.4x; FY28 EBITDA
  ~$71.8B/FCF ~-$17.0B/leverage ~4.8x, improving as expected).
- **Gate 13 (this session, partial): valuation.** See `GATE_13_REVIEW.md` and
  **D-025** in `decision_log.md`. Added a Net Income & EPS bridge to Margin &
  EBITDA (interest, tax at a held-flat 12.6% trailing rate, preferred
  dividends, diluted shares → GAAP EPS) and a new "Valuation (Gate 13)" tab
  to `12_Model/development/ORCL_8Q_Model_v0.4_Gate13.xlsx` (v0.3 archived
  first): NTM revenue/EBITDA/EPS aggregation at the four Framework-specified
  valuation dates, and the enterprise-to-equity bridge components at each
  date's just-completed quarter (Q-11/Q-13 defaults flagged as unresolved,
  not silently settled). **Real multiple assignment left genuinely blank**
  (yellow-highlighted cells) — Q-08/C-09 still block sourcing a real,
  as-of-dated EV/NTM EBITDA or P/NTM EPS multiple; filling it from general
  knowledge would violate the no-fabricated-data rule. An explicitly-labeled
  illustrative-only section (Framework's unadopted 13.0x base midpoint)
  demonstrates the mechanism produces $165.57/share at the first valuation
  date — a sanity signal only, never a price target. Verified via a
  full-chain Python replica matching the actual formulas cell-by-cell.
- **Gate 14 (this session): sensitivities, illustrative multiple.** See
  `GATE_14_REVIEW.md` and **D-026** in `decision_log.md`. Added a
  "Sensitivities (Gate 14)" tab to
  `12_Model/development/ORCL_8Q_Model_v0.5_Gate14.xlsx` (v0.4 archived
  first): Bear/Bull NTM revenue, D&A, and bridge components computed
  directly from the Scenario Assumptions Bear/Bull columns (bypassing the
  single Control-Panel switch, which only drives one case at a time) for a
  genuine three-case comparison at the FY27 Q1 valuation date. **Produced
  the illustrative bear/base/bull price triad the project exists to
  deliver: Bear ~$96/share (10.0x), Base ~$166/share (13.0x), Bull
  ~$244/share (16.0x)** — correctly ordered, using the Framework's own
  unadopted candidate multiples per the user's explicit instruction to
  proceed on that basis. Also added a one-way multiple-sensitivity table
  (9x-17x). Single-valuation-date, closed-form approximation — not a full
  quadrupled quarterly rebuild across all four dates. Q-08/C-09 remain
  unresolved, so all of this stays illustrative until a real multiple is
  sourced. Verified via an independent Python replica matching the actual
  formulas and confirming the bear<base<bull ordering.

## Work in progress

None mid-flight. Clean stopping point.

## Known issues / blockers

1. Q-04: all 8 earnings-call transcripts still missing.
2. Q-05: Oct 16, 2025 analyst-day materials still missing.
3. Q-08: no authenticated consensus/institutional-data source yet (FactSet MCP
   connector present but unauthenticated).
4. Q-11: preferred-security treatment (debt-like vs. as-converted) needs the
   Certificate of Designations/prospectus — not yet obtained.
5. Q-13: lease-in-EV convention still open (Gate 9 resolved Q-12/Q-14 but not
   Q-13 — depends on whether peer multiples used include lease liabilities).
6. SRC-016 capture defect (clipped wide tables in the Q4 FY26 release PDF) -
   cosmetic; never blocked a value.
7. Four blocked reconciliation checks, unchanged since Gate 5B (documented
   reasons, non-blocking): BS_070 non-current deferred-revenue split; CF_040
   acquisitions caption mismatch; CAP_020/commercial-paper Q4 FY26 split;
   FY2025 quarterly debt roll-forward.
8. Pre-Gate-12 action items: four targeted FY26 10-K footnote re-reads
   (useful lives, capitalized interest, BYOH treatment, nonoperating
   investments) — see driver-doc §7.
9. GAAP operating margin still has no ratified scenario range (D-020 covers
   GAAP gross margin and non-GAAP operating margin, not GAAP operating
   margin) — held flat at the FY26 actual through Gate 12; either derive it
   from the historical GAAP/non-GAAP opex bridge or get it ratified.
10. LibreOffice headless recalculation does not work in this sandbox (hangs
    indefinitely even on a trivial one-formula test file, re-confirmed at
    Gate 11 with a 290s budget) — future sessions building on the model
    should verify formulas by opening the file in real Excel/Sheets, or retry
    `scripts/recalc.py` in case a future environment doesn't have this
    limitation.
11. Gate 12's net debt issuance and implied OCF are plugs, not a bottom-up
    build (no issuance schedule or dividend/buyback line is separately
    modeled); the lease-commencement schedule is an even 3-year spread, not
    the real (undisclosed) timing; D-021's fifth control (incremental ROIC)
    is not built — needs an invested-capital base, deferred to Gate 13.
12. Effective tax rate (Margin & EBITDA tab) is held flat at the trailing
    FY26 actual (12.6%) — same gap pattern as GAAP operating margin: no
    ratified D-020 range exists for it.
13. **Gate 13's real multiple assignment is blocked**, not deferred by
    choice: Q-08 (no authenticated consensus/market-data source) and C-09
    (existing comp table stale/single-sourced) mean the "Valuation (Gate 13)"
    tab's multiple cells are intentionally blank. This is the only remaining
    external blocker to producing an actual bear/base/bull price target —
    everything else in the pipeline (revenue → EBITDA → EPS → NTM → EV
    bridge) is built and ready to receive a real multiple.

## Next recommended action

Two paths, either is reasonable: (a) run Gate 15 (investment interpretation)
using the illustrative bear/base/bull range (~$96/$166/$244) as a stand-in,
same illustrative-only caveat carried through; or (b) resolve Q-08 first —
authenticate the FactSet MCP connector, or have the user supply current,
as-of-dated peer market data for the ratified peer set (D-021) — then redo
Gates 13-14 with a real multiple before Gate 15, so the interpretation memo
starts from real numbers instead of illustrative ones.

## Restart note

If this file and the architecture docs disagree, the architecture docs govern
structure; this file governs sequencing/status. For historical values, use
`orcl_historical_quarterly_full.csv` / `_full_provenance.csv` (Gate 6 verified,
zero discrepancies). For forecast driver mechanics, use
`11_Analysis/forecast/GATE7_FORECAST_DRIVER_DESIGN.md` — it references field
IDs, not display labels. The Gate 5A pilot files remain the audit record of
that session only.
