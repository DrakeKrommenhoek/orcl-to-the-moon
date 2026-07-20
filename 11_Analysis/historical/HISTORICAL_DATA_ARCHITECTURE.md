# Historical Data Architecture — Oracle Quarterly Model

Gate: 4 · Date: 2026-07-20 · Status: complete (pending user review)
Companions: `10_Working_Data/architecture/orcl_data_dictionary.csv` (132 fields),
`source_to_field_mapping.csv`, `quarterly_disclosure_matrix.csv`,
`10_Working_Data/templates/orcl_historical_quarterly_template.csv`,
`11_Analysis/historical/HISTORICAL_RECONCILIATION_PLAN.md`,
`10_Working_Data/architecture/EXTRACTION_PRECEDENCE_RULES.md`.

## 1. Historical period covered

**Required:** FY2025 Q1 (Jun–Aug 2024) through FY2026 Q4 (Mar–May 2026) — eight quarters.
**Optional later extension:** FY2024 Q1–Q4 (would require acquiring FY24 quarterly primary
sources; see Q-03 — currently deferred).
**Forecast horizon (structure only, no values in Gate 4):** FY2027 Q1 – FY2028 Q4.
**Valuation checkpoints:** Oracle's next four earnings releases (FY27 Q1, expected
2026-09-10, then FY27 Q2–Q4; dates beyond Q1 are estimates, Q-07).

## 2. Reporting currency and units

- Currency: USD as reported by Oracle. No FX translation of reported figures.
- Flow/stock items: **USD millions** (`USD_m`) exactly as filed; RPO in **USD billions**
  (`USD_b`) because Oracle discloses it in billions.
- Per-share: USD to the cent. Shares: millions (`shares_m`), weighted-average as reported.
- Percentages stored as decimals in data files (0.28, not 28) with `pct` unit tag.
- Sign conventions are per-field in the dictionary (`sign_convention` column); expenses
  and capex are stored positive with direction defined by the field, never re-signed ad hoc.

## 3. Oracle fiscal calendar

FY ends May 31. Q1 ends Aug 31 · Q2 ends Nov 30 · Q3 ends Feb 28/29 · Q4 ends May 31.
Fiscal labels only (`FY2026_Q3` = quarter ended 2026-02-28) — never calendar quarters.
Peer-alignment conventions are a Gate 9 question (Q-12), out of scope here.

## 4. Reported income-statement architecture (Layer 1)

Rows mirror Oracle's filed statements exactly and tie to reported totals:

- Revenue: cloud services and license support (REV_010) · cloud license and on-premise
  license (REV_020) · hardware (REV_030) · services (REV_040) · total (REV_050)
- Expenses: cost lines (COGS_010/020/030), sales & marketing, R&D, G&A, amortization of
  intangibles, acquisition-related, restructuring (OPEX_010–060)
- GAAP operating income (PROF_010), interest expense (PROF_050), non-operating net
  (PROF_060), tax (PROF_080), net income (PROF_100), diluted EPS (PROF_120)
- Non-GAAP operating income / net income / EPS from the release reconciliation tables
  (PROF_030/110/130), stored **with** their reconciling items — never as bare numbers.

**Category-stability caveat (Q-18):** the Research Pack claims Oracle changed headline
revenue presentation in FY26 Q1 (Total Cloud vs. Software). Whether the *filed income
statement* categories changed must be verified during extraction. If filed categories
changed, Layer 1 stores each period **as filed** and a documented mapping (not a silent
restatement) connects the two presentations.

## 5. Supplemental operating-metric architecture (Layer 2)

Only metrics Oracle explicitly discloses, at the granularity disclosed:

- Total cloud revenue (SaaS+IaaS), IaaS dollars/growth, SaaS dollars/growth
  (REV_110–135) — release/slide-level disclosures, confirmed quarter by quarter
- Cloud services vs. license support MD&A split (REV_140/145) — presence per filing TBD
- SBC, depreciation, D&A from cash-flow statements (OPEX_070, PROF_140/150) — YTD basis
- RPO total and %-next-12-months from 10-Q footnotes (RPO_010/020)
- Fusion/NetSuite growth rates (KPI_010/020) — **growth-only; dollar levels are never
  imputed from them**
- Management-defined net cash capex, prepayments, BYOH commentary (CAP_010–030,
  KPI_060/070) — most require the FY26 10-K or transcripts and are marked blocked

## 6. Six-stream analytical revenue architecture (Layer 3; D-005/Q-09)

Forecast streams: **OCI · cloud applications · software support · software licenses ·
hardware · services** (REV_310–360, sum REV_370). This is the forecasting grain; it is
deliberately more granular than Layer 1 and is populated historically *only* via the
bridge below.

## 7. Reported-to-analytical revenue bridge

| Analytical stream | Historical population rule | Basis |
| --- | --- | --- |
| OCI (REV_310) | = disclosed IaaS dollars (REV_120) where disclosed; **else blank ("not disclosed")** | Layer 2 |
| Cloud applications (REV_320) | = disclosed SaaS dollars (REV_130) where disclosed; else blank | Layer 2 |
| Software support (REV_330) | = REV_010 − REV_110 (residual), cross-checked against MD&A license-support line (REV_145) | L1 − L2 |
| Software licenses (REV_340) | = REV_020 (identity) | Layer 1 |
| Hardware (REV_350) | = REV_030 (identity) | Layer 1 |
| Services (REV_360) | = REV_040 (identity) | Layer 1 |

Bridge integrity checks: CHECK_020 (streams sum to reported total), CHECK_030
(IaaS+SaaS = total cloud), CHECK_040 (residual sanity vs. MD&A split). The residual
stream inherits the rounding error of release-level disclosures; it is labeled
`calculated`, never `reported`.

## 8. Cost and margin architecture

Layer 1 expense lines as filed; calculated gross profit/margin (COGS_050/060) under an
explicitly analyst-fixed definition (Oracle presents no gross-profit subtotal).
**No historical OCI-level or stream-level gross margins exist** — COGS_310/320 are
forecast-only drivers and their historical cells are structurally blank (Framework Q16-9).
EBITDA (PROF_160) is defined **nowhere yet**: computation is blocked until the Q-10
definition (SBC, one-time gains like Ampere, lease treatment) is decided and logged.

## 9. Cash-flow architecture

All 10-Q cash-flow figures are **year-to-date**; the architecture stores the YTD value
as filed (CF_010/020/040–090) plus a derived standalone-quarter series (CF_015/025):
Q1 = YTD-Q1 · Q2 = YTD-Q2 − YTD-Q1 · Q3 = YTD-Q3 − YTD-Q2 · Q4 = FY − YTD-Q3.
FCF (CF_030) = standalone OCF − standalone capex, analyst-defined; Oracle's own TTM FCF
table (CF_035) is kept separately for validation and the two are never mixed. Full
derivation and validation rules: `HISTORICAL_RECONCILIATION_PLAN.md`.

## 10. Balance-sheet and financing architecture

Period-end cash, marketable securities, PP&E, ROU assets, deferred revenue, receivables,
equity (BS_010–100); current/noncurrent borrowings with calculated gross and net debt
(DEBT_010–040); operating-lease liabilities (DEBT_050/060); annual-only footnote items —
uncommenced lease commitments (DEBT_070, conflict C-06), maturity schedule, rate mix
(DEBT_080/090); mandatory convertible preferred carrying value and dividends
(DEBT_100/110 — require FY26 10-K + prospectus; treatment decision Q-11). Financing flows
come from the cash-flow statement (CF_050–090). C-01 (FY26 gross debt $135B vs $129.5B)
resolves only when DEBT_030 is computed from the FY26 10-K balance sheet.

## 11. Share-count architecture

Basic and diluted weighted-average shares as reported (SHARE_010/020), dilutive effect
(SHARE_030), period-end cover-page count (SHARE_040), ATM issuance shares/proceeds
(SHARE_050 — FY26 activity requires the 10-K), preferred conversion effect (SHARE_060 —
forecast-only pending Q-11), repurchases (SHARE_070). Forecast dilution mechanics (ATM
price/pace reflexivity) hang off these fields at Gate 7 — no assumptions now.

## 12. RPO and capacity architecture

RPO from the 10-Q revenue-recognition footnote (total + % next-12-months; RPO_010/020),
calculated cRPO (RPO_030, labeled calculated because the % is rounded), growth (RPO_040),
annual duration buckets if disclosed (RPO_050), and an *approximate* implied-bookings
field (RPO_060) whose limitations are stated in the dictionary. Capacity: management-
defined net cash capex, prepayments, short-term financing, BYOH (CAP_010–030) — mostly
FY26-era disclosures requiring the 10-K/transcripts; the forward capacity contribution
index (CAP_050, Q-15) is an analytical construct with **no historical values by design**.

## 13. Quarterly seasonality fields

Seasonality is a *derived view*, not stored data: quarter-share-of-FY ratios computed
from Layer 1/Layer 3 streams at Gate 7 (per Framework §3, with the rule that site-specific
capacity timing overrides historical OCI seasonality). No dedicated fields are hardcoded;
the template's annual columns make the shares computable. This avoids freezing seasonality
"facts" that are actually calculations.

## 14. Forecast handoff requirements

The forecast model (Gates 7+) consumes: the six Layer 3 streams; margin structure
(COGS/OPEX); YTD-free standalone cash-flow series; debt/lease/preferred stack; share
architecture; RPO series; capacity fields; and the VAL_ checkpoint scaffolding (NTM
aggregation at each of the four valuation dates, EV-to-equity bridge per Framework §15).
Field IDs are the stable interface: scripts and spreadsheet ranges reference `REV_310`,
not display labels. Eight forecast quarters map onto the same field set with
`historical_or_forecast` distinguishing population rules.

## 15. Known disclosure limitations

- OCI/SaaS dollars exist only at release/slide level, with independent rounding — not in
  filed statements; availability must be confirmed each quarter.
- Fusion/NetSuite: growth rates only. MultiCloud: growth rates only, recent quarters.
- No stream-level cost or margin disclosure; no capacity units (MW/GPU) disclosure.
- Quarterly depreciation only via YTD cash-flow lines; interest income possibly
  annual-only; CC growth rates are Oracle-computed and unverifiable.
- 10-Q cash flows YTD only (handled in §9); no Q4 10-Q exists (Q4 = release + 10-K).

## 16. Fields that must remain blank historically

Structurally blank (never backfilled): COGS_310/320 (stream gross margins), CAP_050
(capacity index), SHARE_060 (preferred conversion effect), all VAL_ fields, PROF_160
until Q-10 is resolved, and REV_310/320 **in any quarter where Oracle did not disclose
the IaaS/SaaS dollar amount**. Blank means blank — the extraction template's status
column records "not_disclosed", not a proxy value.

## 17. Items requiring the FY2026 10-K (SRC-024 — reserved, not yet received)

FY26 annual anchors for every flow field (sum-of-quarters check); FY26 year-end balance
sheet (C-01 gross debt); FY26 depreciation (C-02); uncommenced lease commitments (C-06);
mandatory convertible terms/carrying value (DEBT_100, Q-11); ATM activity (SHARE_050);
prepayment/short-term-financing disclosures (CAP_010/020); RPO duration buckets (RPO_050);
concentration disclosures (KPI_050); debt maturities/rates (DEBT_080/090).
**Gate 5 extraction of FY26 Q4/annual data is blocked until this document arrives.**
Note: an upload was attempted on 2026-07-20 but the file never reached the session
filesystem — it must be re-provided (ideally committed to `02_Annual_Filings/`).

## 18. Items requiring transcripts or analyst-day materials

Utilization commentary (KPI_030), BYOH/customer-funding statements (KPI_060), net-cash-
capex definitional language (CAP_030 verbatim capture), guidance phrasing for the
guidance-vs-actual table, RPO conversion commentary (C-07 resolution support), long-term
targets incl. FY30 OCI (analyst-day deck, Q-05). All 8 transcripts missing (Q-04).

## 19. Items that should NOT be modeled (insufficient disclosure)

Product-level SaaS P&Ls (Fusion/NetSuite/Oracle Health revenue dollars, margins);
OCI revenue per MW/GPU as a historical series; customer-level RPO or revenue; historical
stream-level gross margins; quarterly interest income (if annual-only); segment-level
capex. These stay qualitative or forecast-assumption territory, clearly labeled.

## How this architecture prevents estimated OCI/SaaS figures becoming "facts"

1. **Three-layer separation**: AI-report estimates satisfy no layer — Layer 1 is filed
   statements, Layer 2 requires an explicit Oracle disclosure, Layer 3 populates only
   through the documented bridge. There is no cell an AI estimate can legally fill.
2. **The disclosure matrix** carries an `EST` code meaning "exists only as a secondary
   estimate — unusable"; the extraction template records `not_disclosed` status instead
   of a value.
3. **Mapping constraint**: `source_to_field_mapping.csv` assigns no AI report as primary
   or secondary source for any financial field (they appear only in conflict notes).
4. **Precedence rules** (`EXTRACTION_PRECEDENCE_RULES.md` §9) rank AI research last and
   prohibit gap-filling with it outright.
5. **Conflict C-03/D-005** already classify the round-number OCI/SaaS series as
   estimates; any attempt to use them must fail the manifest-ID citation requirement.
