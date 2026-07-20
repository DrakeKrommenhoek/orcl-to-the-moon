# Open Questions

Date opened: 2026-07-20. Questions move to `decision_log.md` when resolved.
Conflicts between existing sources live in `source_conflicts.md`, not here.

## A. Blocking before extraction (Gate 5)

- **Q-01** Acquire the FY2026 10-K (FYE 2026-05-31). It is the controlling source for FY26
  balance sheet, leases, debt, depreciation, RPO detail, and financing. URLs in
  `00_MASTER_CHECKLIST.md`. *(Owner: user — sandbox cannot reach sec.gov.)*
- **Q-02** Which provider produced each research .docx (ChatGPT vs. Gemini)? Affects only
  attribution/labeling, not authority rank (both rank 6). *(Owner: user.)*
- **Q-03** Should recast quarterly history start at FY25 Q1 (Framework's recommendation,
  fully covered by current holdings) or FY24 Q1 (Research Pack's span, which would require
  acquiring four FY24 quarterly sources)? *(Recommend FY25 Q1 start; decide at Gate 4.)*
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

- **Q-09** Adopt the Framework's six-stream revenue architecture (OCI, cloud apps, support,
  license, hardware, services) as the canonical recast? *(Recommended; formalize at Gate 4.)*
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
