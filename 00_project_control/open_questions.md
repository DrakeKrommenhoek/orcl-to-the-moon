# Open Questions

Date opened: 2026-07-20. Questions move to `decision_log.md` when resolved.
Conflicts between existing sources live in `source_conflicts.md`, not here.

## A. Blocking before extraction (Gate 5)

- **Q-01** ~~Acquire the FY2026 10-K (FYE 2026-05-31).~~ **Resolved 2026-07-20 (post-Gate-4
  sync session):** the user committed the filing directly to `origin/main` (commit
  `d136102`, "Add files via upload"). It was merged into the working branch, identity
  verified (Form 10-K, Oracle Corporation, Commission File 001-35992, FYE 2026-05-31,
  signed 2026-06-22), moved to `02_Annual_Filings/ORCL_2026_10-K_FY_Ended_2026-05-31.pdf`
  via `git mv`, and registered as **SRC-024** in `source_manifest.csv`. Contents have
  **not** been extracted — that is Gate 5 work, not done in this sync session. C-01,
  C-02, and C-06 remain open until Gate 5/6 extraction and reconciliation.
- **Q-02** Which provider produced each research .docx (ChatGPT vs. Gemini)? Affects only
  attribution/labeling, not authority rank (both rank 6). *(Owner: user.)*
- **Q-03** ~~Should recast quarterly history start at FY25 Q1 or FY24 Q1?~~
  **Settled at Gate 4 (2026-07-20):** required history = FY25 Q1 – FY26 Q4; FY24 is an
  optional later extension that would require acquiring FY24 quarterly sources. Remaining
  open sliver: whether the user wants that extension at all.
- **Q-04** Obtain the 8 earnings-call transcripts (FY25 Q1 – FY26 Q4). *(Owner: user;
  quartr.com link in checklist.)*
- **Q-05** Obtain Oct 16, 2025 Financial Analyst Meeting materials (long-term targets,
  incl. FY30 OCI $144B claim cited in Research Pack). *(Owner: user.)*

## B. Blocking before scenario design (Gates 7–8)

- **Q-06** ~~User must fill in `ORCL_User_Thesis_and_Questions.docx`.~~ **Resolved
  2026-07-21:** thesis captured via clarifying questions and written into the doc.
  Summary — interested on OCI/cloud-infrastructure growth, the multi-cloud database
  moat, and a valuation/mean-reversion setup (fair value seen as significantly above
  current price); 6–18 month holding period; instrument is long calls (max downside =
  full premium); year-end price narrative is multiple expansion to $150, expected
  within 2–3 quarters if not by EOY 2026; invalidation triggers are balance-sheet/
  leverage stress, an AI capex bust, and margin compression from the depreciation
  buildout. Earnings dates aligned to Q-07's canonical set (FY27 Q1 2026-09-10
  management-scheduled; Q2/Q3/Q4 estimates). Gate 8 (scenario approval) unblocked.
- **Q-07** Confirm the four valuation dates. Framework assumes FY27 Q1 release
  2026-09-10 (stated), then est. Dec 2026, Mar 2027, Jun 2027. Only the first is
  management-scheduled; the rest are estimates.
- **Q-08** What consensus source will the model use for quarterly OCI/apps/margin/capex/EPS
  expectations? Public aggregations are too coarse (Framework §11). Options: user-provided
  terminal data, subscription source, or explicitly modeling without consensus overlay.
  Note: a FactSet MCP connector exists in this workspace but is not yet authenticated —
  if the user authorizes it, it may satisfy this need.

**Gate 8 (scenario approval) complete 2026-07-21 → D-020.** The Framework §10
bear/base/bull operating ranges were presented to the user and ratified as
proposed, no adjustments — see `decision_log.md` D-020 and `GATE_8_REVIEW.md`.

## C. Methodology decisions to make (Gates 4, 9)

- **Q-09** ~~Adopt the Framework's six-stream revenue architecture as the canonical
  recast?~~ **Resolved 2026-07-20 → D-009**: adopted as Layer 3 (REV_310–360) with the
  reported-to-analytical bridge in `HISTORICAL_DATA_ARCHITECTURE.md` §7.
- **Q-10** ~~Fix an explicit EBITDA definition (treatment of SBC, leases, Ampere-type gains)
  before any EV/EBITDA work.~~ **Resolved 2026-07-21 → D-014 (ratified):** primary
  EBITDA = GAAP operating income + CF-statement depreciation + amortization of
  intangibles (SBC stays an expense; restructuring stays in; one-time investment
  gains excluded by construction; EBITDA not EBITDAR). User signed off on the
  recommendation as proposed, no adjustments. Full analysis with FY26 numbers in
  `11_Analysis/historical/EBITDA_DEFINITION_MEMO.md`. PROF_160 relabeled ratified
  across all periods.
- **Q-11** ~~Preferred-security treatment: debt-like vs. as-converted.~~ **Substantively
  resolved 2026-07-22 → D-028** (rank-6 sourced, cross-corroborated by two
  independent research tools, not yet independently fetched from the primary
  424B5/FWP): mandatory conversion is not until ~2029-01-15, holders convert
  early only at their own option, and every one of this project's four
  valuation dates (2026-09 through 2027-06) falls well before that date — so
  **debt-like treatment (subtract preferred value, exclude conversion shares,
  include preferred dividends in common income) is the structurally correct
  choice for all four valuation checkpoints**, not merely a default pending
  resolution. This is exactly what the model already did (Gates 12-14). The
  "as-converted" question only becomes live for any valuation date at or
  after Jan 2029, which is outside this project's scope. See `decision_log.md`
  D-028 and `source_conflicts.md`'s confirmed-consistencies note.
- **Q-12** ~~NTM window convention for Oracle vs. peers with different fiscal year
  ends.~~ **Resolved 2026-07-21 → D-021 (Gate 9, ratified):** every company's NTM
  window built on a calendar-quarter basis; peer fiscal-quarter data interpolated
  onto calendar quarters rather than comparing "next four fiscal quarters" as each
  company defines them. See `11_Analysis/valuation/GATE9_COMPS_METHODOLOGY.md` §3.
- **Q-13** Lease treatment convention in EV and leverage (include lease liabilities in EV
  bridge only if peer multiples use the same convention).
- **Q-14** ~~Peer-set weighting: how much anchor weight to Amazon/Alphabet.~~
  **Resolved 2026-07-21 → D-021 (Gate 9, ratified):** weighted down rather than
  excluded — Microsoft ~50%, Amazon ~25%, Alphabet ~25% within the OCI peer
  reference; CoreWeave confirmed reference-only. See `GATE9_COMPS_METHODOLOGY.md`
  §2.
- **Q-15** ~~Capacity-based OCI forecast requires a "capacity contribution index".~~
  **Recommendation issued 2026-07-21 (Gate 7 → D-019, provisional):** a relative,
  unitless index rebased to FY26 Q4 = 100, built from net PP&E growth attributable
  to the buildout, reconciled quarterly against disclosed site additions/RPO/lease-
  commencement anchors. See `11_Analysis/forecast/GATE7_FORECAST_DRIVER_DESIGN.md`
  §4. Provisional pending user sign-off (same pattern as D-014); does not block
  Gate 8.

## D. Substantive modeling unknowns (inherited from Framework §16 — kept as the master list)

The Framework's 30 unresolved questions (customer-level RPO mix, contract terms,
in-service dates, revenue per unit of capacity, useful lives, ATM execution pace,
convertible EPS treatment, tax rate, capitalized interest, Oracle Health profitability,
support durability, etc.) are adopted wholesale as the substantive research agenda. See
`01_Research_Outputs/ORCL_Eight_Quarter_Model_Framework_2026-07-20.docx` §16.
**Triaged 2026-07-21 (Gate 7):** full item-by-item disposition in
`11_Analysis/forecast/GATE7_FORECAST_DRIVER_DESIGN.md` §2. Summary: 8 are
permanently assumption/scenario-input by design (capacity-unit economics, ATM
pricing, future debt terms, customer-level RPO mix, etc.); 10 are partially
answerable from documents already in the repo (a short list of FY26 10-K
footnote re-reads before Gate 10 — useful lives, capitalized interest, BYOH
treatment, nonoperating investments); 2 need a specific new document/connector
already tracked (Q-11, Q-08); the rest are resolved or bounded by data already
extracted (effective tax rate, support-revenue stability, aggregate prepayment/
BYOH figures).

## E. Workspace / process

- **Q-16** Large-file strategy if the repo grows (Git LFS threshold, see README §Version
  control). Current ~50 MB is fine.
- **Q-17** Should prior-quarter earnings slide decks (FY25 Q1 – FY26 Q3) be acquired?
  Checklist marks optional; guidance slides would strengthen the guidance-history table.

- **Q-18** *(added 2026-07-20, Gate 4)* ~~Did Oracle's FY26 Q1+ reporting change alter the
  *filed income-statement* revenue categories, or only headline/release presentation?~~
  **RESOLVED 2026-07-20 (Gate 5A).** It is a **true reclassification of the filed
  income statement**, effective FY26 Q1, with prior-year comparatives recast — not a
  headline-only change. Evidence: SRC-006 statements (PDF p.7) present revenues as
  Cloud / Software / Hardware / Services vs. SRC-003's Cloud services and license
  support / Cloud license and on-premise license / Hardware / Services; SRC-006 Note 1
  (p.11) states "We reclassed certain revenues and other related disclosures to conform
  to the current period's presentation for all periods presented... did not affect total
  revenue, income from operations or net income." Recast ties exactly (FY25 Q1: Cloud
  5,623 + Software 5,766 = 11,389 = 10,519 + 870). Component detail moved to a new
  "revenues by offerings" footnote (Software license / Software support; Cloud
  applications / Cloud infrastructure — now exact millions, an upgrade). Expense side:
  "Cloud services and license support" → "Cloud and software" is a **relabel only**
  (prior-year value 2,597 unchanged). Two further changes inside FY26: (i) the 10-K
  annual statement (and Q4 release) merge "Acquisition related and other" +
  "Restructuring" into **"Restructuring and other"** (recast: FY25 75+299=374) while
  FY26 10-Qs kept separate lines; (ii) from Q3 FY26 a **"Preferred stock dividends"**
  line and "Net income available to common shareholders" subtotal appear, and EPS is
  now "attributable to common shareholders." Architecture response: dual-presentation
  Layer 1 via new fields REV_011/REV_021/COGS_011/OPEX_065/REV_147 with documented
  bridge (D-013); each period stored as filed; no silent restatement of FY25 rows.
