# CURRENT_STATE

Last updated: 2026-07-21 (Gate 8 scenario approval session)
Branch: `claude/oracle-historical-extraction-handoff-7dn6cr` (remote =
DrakeKrommenhoek/orcl-to-the-moon). Rebuilt 2026-07-21 on top of
`claude/oracle-historical-extraction-pilot-r6o3ov`, which carries the actual
Gate 5A/5B/6 work — the originally assigned handoff branch had been deleted
upstream with no PR ever opened, so this session restarted it from the branch
that actually held the completed work.

## Current phase

**Gate 8 (scenario approval) COMPLETE.** Gates 1-7 complete (see below).
**Next: Gate 9 (comps methodology).**

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

## Work in progress

None mid-flight. Clean stopping point.

## Known issues / blockers

1. Q-04: all 8 earnings-call transcripts still missing.
2. Q-05: Oct 16, 2025 analyst-day materials still missing.
3. Q-08: no authenticated consensus/institutional-data source yet (FactSet MCP
   connector present but unauthenticated).
4. Q-11: preferred-security treatment (debt-like vs. as-converted) needs the
   Certificate of Designations/prospectus — not yet obtained.
5. Q-12/Q-13/Q-14: NTM-alignment convention, lease-in-EV convention, and peer
   weighting are open Gate 9 methodology decisions.
6. SRC-016 capture defect (clipped wide tables in the Q4 FY26 release PDF) -
   cosmetic; never blocked a value.
7. Four blocked reconciliation checks, unchanged since Gate 5B (documented
   reasons, non-blocking): BS_070 non-current deferred-revenue split; CF_040
   acquisitions caption mismatch; CAP_020/commercial-paper Q4 FY26 split;
   FY2025 quarterly debt roll-forward.
8. Pre-Gate-10 action items (not blocking Gate 8/9): four targeted FY26 10-K
   footnote re-reads (useful lives, capitalized interest, BYOH treatment,
   nonoperating investments) — see driver-doc §7.

## Next recommended action

Run Gate 9 (comps methodology) using the exact prompt in
`00_project_control/GATE_8_REVIEW.md` §4. Needs to resolve NTM-window
alignment (Q-12), peer weighting (Q-14), the primary valuation methodology/
multiple framework (Framework §7-8), and re-source the comp table's market
data with explicit as-of dates (C-09).

## Restart note

If this file and the architecture docs disagree, the architecture docs govern
structure; this file governs sequencing/status. For historical values, use
`orcl_historical_quarterly_full.csv` / `_full_provenance.csv` (Gate 6 verified,
zero discrepancies). For forecast driver mechanics, use
`11_Analysis/forecast/GATE7_FORECAST_DRIVER_DESIGN.md` — it references field
IDs, not display labels. The Gate 5A pilot files remain the audit record of
that session only.
