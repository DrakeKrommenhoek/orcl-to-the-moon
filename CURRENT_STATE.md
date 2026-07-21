# CURRENT_STATE

Last updated: 2026-07-21 (Gate 10 minimal model build session)
Branch: `claude/oracle-historical-extraction-handoff-7dn6cr` (remote =
DrakeKrommenhoek/orcl-to-the-moon). Rebuilt 2026-07-21 on top of
`claude/oracle-historical-extraction-pilot-r6o3ov`, which carries the actual
Gate 5A/5B/6 work — the originally assigned handoff branch had been deleted
upstream with no PR ever opened, so this session restarted it from the branch
that actually held the completed work.

## Current phase

**Gate 10 (minimal model build) COMPLETE.** Gates 1-9 complete (see below).
**Next: Gate 11 (model checks).**

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
9. GAAP operating margin has no ratified scenario range (D-020 covers GAAP
   gross margin and non-GAAP operating margin, not GAAP operating margin) —
   held flat at the FY26 actual in the Gate 10 model; Gate 12 should either
   derive it from the historical GAAP/non-GAAP opex bridge or get it ratified.
10. LibreOffice headless recalculation does not work in this sandbox (hangs
    indefinitely even on a trivial one-formula test file) — future sessions
    building on the model should verify formulas by opening the file in real
    Excel/Sheets, or retry `scripts/recalc.py` in case a future environment
    doesn't have this limitation.

## Next recommended action

Run Gate 11 (model checks) per `GATE_10_REVIEW.md` §4: get real formula
recalculation confirmed (ideally in an environment where LibreOffice works,
or via the user opening the file), expand the Checks tab toward the full
CHECK_ family once Gate 12 adds balance-sheet/cash-flow schedules, and close
the GAAP-operating-margin gap noted above.

## Restart note

If this file and the architecture docs disagree, the architecture docs govern
structure; this file governs sequencing/status. For historical values, use
`orcl_historical_quarterly_full.csv` / `_full_provenance.csv` (Gate 6 verified,
zero discrepancies). For forecast driver mechanics, use
`11_Analysis/forecast/GATE7_FORECAST_DRIVER_DESIGN.md` — it references field
IDs, not display labels. The Gate 5A pilot files remain the audit record of
that session only.
