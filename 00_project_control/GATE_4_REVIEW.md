# Gate 4 Review — Historical-Data Architecture

Date: 2026-07-20 · Session: Gate 4 only (no extraction, no forecasting, no valuation)

> **Addendum (2026-07-20, post-Gate-4 branch-sync session):** the FY2026 10-K referenced
> below as "missing"/"reserved" has since been supplied — the user committed it to
> `origin/main` (commit `d136102`), it was merged into this working branch, identity was
> verified (Form 10-K, Oracle Corporation, FYE 2026-05-31, Commission File 001-35992,
> signed 2026-06-22), and it is now registered as **SRC-024** at
> `02_Annual_Filings/ORCL_2026_10-K_FY_Ended_2026-05-31.pdf`. Its *contents* have not been
> extracted — §6, §8, §9, §12, §13 below describe the pre-sync state and are otherwise
> left as originally written; treat every "blocked on SRC-024 arriving" statement below as
> now "blocked on SRC-024 *extraction*," which is Gate 5 work, not yet performed.

## 1. Files reviewed

`CLAUDE.md`, `README.md`, `CURRENT_STATE.md`, `00_project_control/*` (all), git state
(clean tree, branch `claude/oracle-equity-model-mhmjq4` tracking origin, remote =
`DrakeKrommenhoek/orcl-to-the-moon` via session git proxy — confirmed). Both AI research
documents were already fully read in the Gates 1–3 session; no source file was opened
for numeric extraction this session.

## 2. Files created

| File | Purpose |
| --- | --- |
| `11_Analysis/historical/HISTORICAL_DATA_ARCHITECTURE.md` | 19-section architecture (3-layer design) |
| `11_Analysis/historical/HISTORICAL_RECONCILIATION_PLAN.md` | Gate 6 validation spec incl. YTD differencing |
| `10_Working_Data/architecture/orcl_data_dictionary.csv` | 132 fields, 26 attributes each |
| `10_Working_Data/architecture/source_to_field_mapping.csv` | 132 rows, 1:1 with dictionary |
| `10_Working_Data/architecture/quarterly_disclosure_matrix.csv` | 63 key fields × 8 quarters, coded |
| `10_Working_Data/architecture/EXTRACTION_PRECEDENCE_RULES.md` | 9-rung ladder + 12 handling rules |
| `10_Working_Data/templates/orcl_historical_quarterly_template.csv` | 120 extractable rows, no values |
| `00_project_control/GATE_4_REVIEW.md` | This document |

Updated: `CURRENT_STATE.md`, `CHANGELOG.md`, `decision_log.md` (D-009…D-012),
`open_questions.md` (Q-18 added; Q-01 updated), `source_conflicts.md` (resolution
procedures annotated on C-01/C-02/C-06).

## 3. Architecture decisions made (logged as D-009…D-012)

- **Three-layer separation** (D-009): L1 as-filed statements · L2 explicit supplemental
  disclosures · L3 analytical streams populated only via a documented bridge.
- **YTD handling** (D-010): as-filed YTD fields + derived standalone fields; formulas fixed.
- **Blank-beats-guess** (D-011): undisclosed history stays blank/`not_disclosed`; AI
  estimates barred from all layers; rounded disclosures keep stated precision.
- **Stable field IDs** (D-012): 13 families, IDs are the interface for scripts/Excel.

## 4. Revenue streams selected (per D-005/Q-09)

OCI · cloud applications · software support · software licenses · hardware · services
(REV_310–360). Ratified as the Layer 3 forecasting grain.

## 5. Reported-to-analytical bridge

OCI = disclosed IaaS dollars; apps = disclosed SaaS dollars; support = REV_010 − total
cloud (residual, cross-checked vs. MD&A split); license/hardware/services = identities to
L1. Integrity checks CHECK_020/030/040. Residual labeled `calculated`.

## 6. Fields that cannot be historically populated

Structurally blank: COGS_310/320, CAP_050, SHARE_060, all VAL_ fields, PROF_160 (until
Q-10), REV_310/320 in any quarter lacking the IaaS/SaaS dollar disclosure. Blocked
pending missing sources: DEBT_070/100/110, SHARE_050, KPI_030/060/070, CAP_010/020
(FY26 10-K and/or transcripts); several annual-only fields are FY25-populatable from
SRC-002 but FY26-blocked (BS_050, DEBT_080/090, RPO_050, CAP_040/060, KPI_050, PROF_065).

## 7. Required formulas for later extraction

YTD differencing (Q1=YTD1; Q2=YTD2−YTD1; Q3=YTD3−YTD2; Q4=FY−YTD3); Q4 P&L = Q4 release
figures validated vs. FY−9M; residual support bridge; cRPO = RPO × %; net debt, gross
debt, EPS-tie, debt roll-forward, cash tie — all specified in the reconciliation plan
and dictionary `calculation_method` column. None executed yet.

## 8. Source gaps

FY26 10-K (SRC-024 reserved — **the attached file did not reach this session's
filesystem; re-provide**), 8 transcripts, analyst-day deck, filled thesis, FY24
quarterlies (only if Q-03 extends history), verifiable market data (Gate 9).

## 9. Remaining conflicts

C-01…C-11 all open. Gate 4 assigned each numeric conflict a designated resolution test:
C-01 → DEBT_030 from FY26 10-K; C-02 → PROF_140 annual tie; C-06 → DEBT_070 footnote;
C-07 → RPO footnote series. None resolvable without SRC-024.

## 10. Items requiring user judgment

(a) Re-provide the FY26 10-K (upload didn't land — committing the PDF to
`02_Annual_Filings/` is most reliable); (b) fill the thesis template (Q-06); (c) confirm
research-report provider attribution (Q-02); (d) decide FY24 extension (Q-03); (e)
transcripts/analyst-day acquisition (Q-04/Q-05); (f) later: EBITDA definition sign-off
(Q-10) and preferred treatment (Q-11) — analyst will propose, user approves.

## 11. Is Gate 4 complete?

**Yes** — all eight deliverables exist, CSVs pass structural validation (unique IDs,
1:1 dictionary↔mapping, matrix rows resolve, no financial values anywhere), and the
architecture supports 8 historical + 8 forecast quarters + 4 valuation checkpoints.

## 12. Is Gate 5 ready to begin?

**Partially.** FY25 Q1 – FY26 Q3 extraction can start now (10-Qs + releases in repo).
FY26 Q4/annual extraction and all C-01/C-02/C-06 resolution are **blocked on SRC-024**.

## 13. Conditions before Gate 5 starts

Required: FY26 10-K present in `02_Annual_Filings/` and registered as SRC-024 (for the
full-scope Gate 5). Acceptable interim: begin Gate 5 for FY25Q1–FY26Q3 + FY26 Q4
release-level only, with FY26 annual ties deferred. Recommended-not-blocking:
transcripts, filled thesis.

## 14. Recommended next prompt

See `CURRENT_STATE.md` §"Exact restart prompt" (Gate 5 extraction prompt).
