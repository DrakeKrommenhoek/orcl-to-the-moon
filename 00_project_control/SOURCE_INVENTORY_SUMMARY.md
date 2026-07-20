# Source Inventory Summary

Date: 2026-07-20 (organizational pass, Gates 1–3)
Machine-readable companion: `source_manifest.csv`

## File counts by type

| Type | Count | Notes |
| --- | --- | --- |
| 10-K annual filings | 2 | FY2024, FY2025 |
| 10-Q quarterly filings | 6 | FY25 Q1–Q3, FY26 Q1–Q3 |
| Earnings releases | 8 | FY25 Q1 – FY26 Q4 (complete eight-quarter run) |
| Earnings slide decks | 1 | FY26 Q4 only |
| Financing announcements | 1 | CY2026 Equity & Debt Financing Plan (2026-02-01) |
| AI research reports (.docx) | 2 | Both dated 2026-07-20; provider attribution unresolved |
| User thesis document | 1 | **Blank template — not filled in** |
| Peer reference index | 1 | Pointer document, no financial data |
| Project-control docs | 1 | 00_MASTER_CHECKLIST.md (from prior session) |
| Spreadsheets | 0 | None exist yet (correct for current gate) |
| Python scripts | 0 | None exist yet |
| Transcripts | 0 | **All missing** |
| **Total files** | **23** | ~50 MB, all verified against filenames |

- Oracle primary sources: **18** (all verified: page-1 content matches filename claims)
- Peer-company primary sources: **0** (deliberate per checklist — deferred until a specific number needs checking)
- Research reports: **2** substantive + 1 index
- Suspected duplicate groups: **0** (MD5-verified across all PDFs)

## Missing expected materials (vs. 00_MASTER_CHECKLIST.md and project needs)

Ranked by importance:

1. **ORCL FY2026 10-K (FYE 2026-05-31)** — the checklist calls this "most important —
   controlling historical source." Its absence blocks verification of FY26 debt, leases
   (~$260B uncommenced lease commitments claim), depreciation, RPO detail, and financing
   activity. Direct URLs are in the checklist. **Highest-priority acquisition.**
2. **Earnings-call transcripts, FY25 Q1 – FY26 Q4 (all 8)** — needed for guidance
   language, utilization/capacity commentary, and RPO conversion discussion.
3. **2025 Financial Analyst Meeting materials (Oct 16, 2025)** — source for long-term
   targets (e.g., FY30 OCI revenue target cited in research reports).
4. **ChatGPT / Gemini deep-research PDFs as named in checklist** — likely satisfied by
   the two .docx files in `01_Research_Outputs/`, but provider attribution is unconfirmed.
5. **Filled-in user thesis** (`ORCL_User_Thesis_and_Questions.docx` is an empty template)
   — required before scenario approval (Gate 8) and instrument selection.
6. **FY2024 quarterly primary sources** — the research pack presents FY24 Q1–Q4 quarterly
   figures, but the repo has no FY24 10-Qs or earnings releases to verify them. Needed only
   if the model's recast history extends to FY24 (framework doc suggests history starting
   FY25 Q1, which the current holdings cover).
7. **Prior-quarter earnings slide decks** (FY25 Q1 – FY26 Q3) — checklist marks optional.
8. **Market-data snapshot with as-of dates** — comp-table market data currently exists only
   inside the research pack (as-of 2026-07-17/20, single-sourced, unverified).

## Stale or undated materials

- Comp market data in the research pack is as-of 2026-07-17/20 — acceptable today but will
  be stale by the first valuation date (FY27 Q1 earnings, ~2026-09-10). Must be refreshed
  from a verifiable market-data source at model time.
- `ORCL_FY2026_Q4_Earnings_Slides.pdf` has no download stamp (native PDF); presentation
  date 2026-06-10 from the title slide.
- Neither .docx research report states its provider; both state research date 2026-07-20.

## Files that could not be interpreted

None. All 23 files were opened and identified.

## Interpretation notes

- All SEC/IR PDFs are browser print-to-PDF captures (stamped 7/20/26) of HTML pages, not
  EDGAR-native PDFs. Fine for reading; pagination in citations should reference section
  names rather than printed page numbers where possible.
- There are no 10-Qs for fiscal Q4s — correct, since 10-Ks cover Q4; Q4 quarterly figures
  must be derived as FY minus 9-month figures during extraction.
