# Gate 8 Review — Scenario Approval

Date: 2026-07-21 · Session scope: present the Framework §9/§10 bear/base/bull
operating-scenario definitions and numeric ranges to the user for explicit
review against the ratified thesis (D-018), and log the user's decision.
Branch: `claude/oracle-historical-extraction-handoff-7dn6cr`.

## 1. What Gate 8 did

Presented, in chat, the Framework's qualitative bear/base/bull differentiators
(capacity delivery timing, OCI/applications growth, margins, financing/
dilution posture, credit trajectory) and the full numeric ranges table (FY27
and FY28, twelve driver rows) reproduced from
`01_Research_Outputs/ORCL_Eight_Quarter_Model_Framework_2026-07-20.docx` §10.
Flagged explicitly that the user's $150 price target rests on a *multiple*
assumption applied to an operating case's NTM EBITDA — a separate Gate 9/13
decision — not something this gate resolves. Asked the user two things: (a)
whether to approve the ranges as-is, adjust them, or discuss trade-offs first;
(b) whether the Bear case's severity adequately represents their stated
invalidation triggers (balance-sheet/leverage stress, an AI capex bust, margin
compression — from D-018).

## 2. User decision

**Approved as proposed, no adjustments to any driver or range.** Confirmed
the Bear case's severity (OCI gross margin below 30%, additional debt/ATM
dilution at a depressed share price, deeply negative free cash flow, further
credit-metric deterioration) is an adequate representation of their exit
triggers. Logged as **D-020** in `decision_log.md`, with the full ratified
table reproduced there for a single source of truth (no second copy to drift
out of sync — Gate 10 build must read from D-020, not re-derive from the
Framework docx).

## 3. What remains open

- The capacity-contribution-index definition (D-019, Q-15) is still
  provisional pending separate confirmation — not part of what was ratified
  here, since it is a mechanical construct, not a scenario range.
- Q-11 (preferred treatment), Q-12 (NTM alignment), Q-13 (lease convention),
  Q-14 (peer weighting) are unresolved Gate 9 methodology decisions.
- The multiple/valuation assumption (EV/EBITDA or P/E level applied at each
  scenario, per Framework §7-8) that turns a ratified operating case into a
  per-share number is not decided yet — that is Gate 9 (comps methodology)
  and Gate 13 (valuation), not Gate 8.
- Q-08 (consensus source), Q-04/Q-05 (transcripts/analyst day) remain open,
  non-blocking for Gate 9.

## 4. Exact next prompt (Gate 9)

> Continue the Oracle equity-research project. This session is Gate 9: comps
> methodology. Read CLAUDE.md, CURRENT_STATE.md, 00_project_control/
> (especially this file, decision_log.md's D-020, and open_questions.md's
> Q-08/Q-09/Q-12/Q-14 family), `11_Analysis/forecast/
> GATE7_FORECAST_DRIVER_DESIGN.md`, and the comps framing in
> `01_Research_Outputs/ORCL_Eight_Quarter_Model_Framework_2026-07-20.docx`
> §6-8. Resolve: the NTM-window alignment convention across Oracle's and each
> peer's differing fiscal year ends (Q-12); peer-set weighting given the two
> AI research reports disagree on Amazon/Alphabet emphasis (Q-14, C-09); the
> primary valuation methodology and multiple framework (EV/NTM EBITDA vs.
> P/NTM EPS vs. shadow SOTP) per Framework §7-8; and re-source the comp
> table's market data with explicit as-of dates (C-09 flags the existing
> comp table as illustrative-only, single-sourced). Do not assign scenario
> multiples yet if that requires unauthenticated consensus data (Q-08) —
> flag what's blocked. Do not begin any model build (Gate 10). Update
> project-control files, commit, and push on the designated branch.
