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

- **Q-06** User must fill in `ORCL_User_Thesis_and_Questions.docx`: why Oracle, holding
  period, price narrative, invalidation triggers, instrument (stock/calls/spread), max
  downside, and the four earnings dates for price targets.
- **Q-07** Confirm the four valuation dates. Framework assumes FY27 Q1 release
  2026-09-10 (stated), then est. Dec 2026, Mar 2027, Jun 2027. Only the first is
  management-scheduled; the rest are estimates.
- **Q-08** What consensus source will the model use for quarterly OCI/apps/margin/capex/EPS
  expectations? Public aggregations are too coarse (Framework §11). Options: user-provided
  terminal data, subscription source, or explicitly modeling without consensus overlay.
  Note: a FactSet MCP connector exists in this workspace but is not yet authenticated —
  if the user authorizes it, it may satisfy this need.

## C. Methodology decisions to make (Gates 4, 9)

- **Q-09** ~~Adopt the Framework's six-stream revenue architecture as the canonical
  recast?~~ **Resolved 2026-07-20 → D-009**: adopted as Layer 3 (REV_310–360) with the
  reported-to-analytical bridge in `HISTORICAL_DATA_ARCHITECTURE.md` §7.
- **Q-10** Fix an explicit EBITDA definition (treatment of SBC, leases, Ampere-type gains)
  before any EV/EBITDA work.
- **Q-11** Preferred-security treatment: debt-like vs. as-converted (Framework §15 rules
  out mixing both). Decide once terms are verified from the 8-A/prospectus.
- **Q-12** NTM window convention for Oracle vs. peers with different fiscal year ends (C-10).
- **Q-13** Lease treatment convention in EV and leverage (include lease liabilities in EV
  bridge only if peer multiples use the same convention).
- **Q-14** Peer-set weighting: how much anchor weight to Amazon/Alphabet given the two AI
  reports disagree (C-09); CoreWeave stays reference-only (both agree).
- **Q-15** Capacity-based OCI forecast requires a "capacity contribution index" (Framework
  §2) — define its units and reconciliation procedure to disclosed site additions and RPO
  commencements.

## D. Substantive modeling unknowns (inherited from Framework §16 — kept as the master list)

The Framework's 30 unresolved questions (customer-level RPO mix, contract terms,
in-service dates, revenue per unit of capacity, useful lives, ATM execution pace,
convertible EPS treatment, tax rate, capitalized interest, Oracle Health profitability,
support durability, etc.) are adopted wholesale as the substantive research agenda. See
`01_Research_Outputs/ORCL_Eight_Quarter_Model_Framework_2026-07-20.docx` §16. They will be
triaged into answerable-from-filings vs. permanently-assumption-based during Gate 7.

## E. Workspace / process

- **Q-16** Large-file strategy if the repo grows (Git LFS threshold, see README §Version
  control). Current ~50 MB is fine.
- **Q-17** Should prior-quarter earnings slide decks (FY25 Q1 – FY26 Q3) be acquired?
  Checklist marks optional; guidance slides would strengthen the guidance-history table.

- **Q-18** *(added 2026-07-20, Gate 4)* Did Oracle's FY26 Q1+ reporting change alter the
  *filed income-statement* revenue categories, or only headline/release presentation
  (Research Pack claims a Total Cloud vs. Software regrouping — C-04)? Determines whether
  Layer 1 needs a dual-presentation mapping across FY25/FY26. Resolve at Gate 5 by
  inspecting SRC-006 (FY26 Q1 10-Q) statement captions vs. SRC-003 (FY25 Q1).
