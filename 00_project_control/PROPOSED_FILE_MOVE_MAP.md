# Proposed File Move Map

Date: 2026-07-20
Prepared during: Gate 1–3 organizational pass
Status: PROPOSED → EXECUTED (high-confidence moves only; see "Execution notes" at bottom)

## Rationale

The workspace was set up by an earlier Claude session around a numbered folder plan
documented in `00_MASTER_CHECKLIST.md` (folders `01_Research_Outputs/` through
`09_Comparable_Companies/`). The user then downloaded the source PDFs but dropped them
into the repository root instead of the planned subfolders. Because the checklist's
structure is intentional, logical, and the PDF filenames already match its exact naming
convention, the reorganization **adopts the checklist's numbered structure** rather than
imposing a new one. `00_project_control/` is added for project-governance files, and
working-data / analysis / model folders will be added later (as `10_`+ numbered folders)
when those process gates are reached — no empty folders are created now.

All moves are performed with `git mv` (history-preserving, fully reversible). Nothing is
deleted, converted, or edited. Original source files remain byte-identical.

## Move map

| Current path | Proposed path | Proposed filename | Reason | Confidence | Action needed |
| --- | --- | --- | --- | --- | --- |
| `00_MASTER_CHECKLIST.md` | `00_project_control/00_MASTER_CHECKLIST.md` | unchanged | Project-control document; belongs with governance files | High | **Move** |
| `Oracle 2024 10K.pdf` | `02_Annual_Filings/ORCL_2024_10-K_FY_Ended_2024-05-31.pdf` | renamed | Checklist specifies this exact target name; FYE 2024-05-31 verified on page 1 of the PDF; spaces removed for tooling | High | **Move + Rename** |
| `Oracle 2025 10K.pdf` | `02_Annual_Filings/ORCL_2025_10-K_FY_Ended_2025-05-31.pdf` | renamed | Checklist specifies this exact target name; FYE 2025-05-31 verified on page 1 of the PDF | High | **Move + Rename** |
| `ORCL_FY2025_Q1_10-Q_2024-08-31.pdf` | `03_Quarterly_Filings/` (same filename) | unchanged | Matches checklist name and destination exactly | High | **Move** |
| `ORCL_FY2025_Q2_10-Q_2024-11-30.pdf` | `03_Quarterly_Filings/` | unchanged | Same | High | **Move** |
| `ORCL_FY2025_Q3_10-Q_2025-02-28.pdf` | `03_Quarterly_Filings/` | unchanged | Same | High | **Move** |
| `ORCL_FY2026_Q1_10-Q_2025-08-31.pdf` | `03_Quarterly_Filings/` | unchanged | Same | High | **Move** |
| `ORCL_FY2026_Q2_10-Q_2025-11-30.pdf` | `03_Quarterly_Filings/` | unchanged | Same | High | **Move** |
| `ORCL_FY2026_Q3_10-Q_2026-02-28.pdf` | `03_Quarterly_Filings/` | unchanged | Same | High | **Move** |
| `ORCL_FY2025_Q1_Earnings_Release_2024-09-09.pdf` | `04_Earnings_Releases/` | unchanged | Matches checklist name and destination | High | **Move** |
| `ORCL_FY2025_Q2_Earnings_Release_2024-12-09.pdf` | `04_Earnings_Releases/` | unchanged | Same | High | **Move** |
| `ORCL_FY2025_Q3_Earnings_Release_2025-03-10.pdf` | `04_Earnings_Releases/` | unchanged | Same | High | **Move** |
| `ORCL_FY2025_Q4_Earnings_Release_2025-06-11.pdf` | `04_Earnings_Releases/` | unchanged | Same | High | **Move** |
| `ORCL_FY2026_Q1_Earnings_Release_2025-09-09.pdf` | `04_Earnings_Releases/` | unchanged | Same | High | **Move** |
| `ORCL_FY2026_Q2_Earnings_Release_2025-12-10.pdf` | `04_Earnings_Releases/` | unchanged | Same | High | **Move** |
| `ORCL_FY2026_Q3_Earnings_Release_2026-03-10.pdf` | `04_Earnings_Releases/` | unchanged | Same | High | **Move** |
| `ORCL_FY2026_Q4_Earnings_Release_2026-06-10.pdf` | `04_Earnings_Releases/` | unchanged | Same | High | **Move** |
| `ORCL_FY2026_Q4_Earnings_Slides.pdf` | `05_Earnings_Slides/` | unchanged | Matches checklist name and destination | High | **Move** |
| `ORCL_2026_Equity_and_Debt_Financing_Plan.pdf` | `06_Financing_Capital_Structure/` | unchanged | Matches checklist name and destination; publication date Feb 1, 2026 verified on page 1 | High | **Move** |
| `Oracle Corporation (ORCL) Public-Markets Research Pack.docx` | `01_Research_Outputs/ORCL_Public_Markets_Research_Pack_2026-07-20.docx` | renamed | AI deep-research output belongs in Research_Outputs; renamed to project convention (ORCL prefix, as-of date from document header, no spaces/parentheses). **Provider (ChatGPT vs. Gemini) not stated in the file — attribution unresolved, see open_questions.md** | Medium-High | **Move + Rename; needs review** (provider attribution) |
| `Oracle_Deep_Research_Eight_Quarter_Model_Framework.docx` | `01_Research_Outputs/ORCL_Eight_Quarter_Model_Framework_2026-07-20.docx` | renamed | Same rationale; research date 2026-07-20 stated in document. **Provider not stated — attribution unresolved** | Medium-High | **Move + Rename; needs review** (provider attribution) |
| `01_Research_Outputs/ORCL_User_Thesis_and_Questions.docx` | unchanged | unchanged | Correct location per checklist. **File is a blank template — user must fill it in before scenario design (Gate 8)** | High | **Keep in place; needs user input** |
| `09_Comparable_Companies/ORCL_Comparable_Company_Source_Index.docx` | unchanged | unchanged | Correct location per checklist | High | **Keep in place** |

## Duplicates

MD5 hashing of all 18 PDFs found **no duplicate or near-duplicate files**. All file
sizes and hashes are distinct. The four .docx files are all distinct documents.

One *conceptual* duplication risk: the checklist expects
`ORCL_ChatGPT_Deep_Research_2026-07-20.pdf` and `ORCL_Gemini_Deep_Research_2026-07-20.pdf`.
The two root .docx research documents are almost certainly these two deliverables saved
as .docx instead of .pdf (both carry the same 2026-07-20 research date). They are treated
as satisfying those checklist slots pending user confirmation of which provider produced
which document.

## Folders intentionally NOT created (missing materials)

| Planned folder | Why not created |
| --- | --- |
| `07_Analyst_Day/` | No analyst-day materials present (Oct 16, 2025 Financial Analyst Meeting deck missing) |
| `08_Earnings_Call_Transcripts/` | No transcripts present (all 8 quarters FY25 Q1 – FY26 Q4 missing) |
| `10_Working_Data/`, `11_Analysis/`, `12_Model/`, `13_Deliverables/`, `99_Archive/` | Reserved for later process gates (extraction, analysis, model build); will be created when first needed |

## Execution notes

All rows marked High or Medium-High confidence were executed with `git mv` in the same
commit that adds this file. No file contents were modified. The two Medium-High renames
are content-neutral (rename only) and reversible via git history; the unresolved item on
them is provider *attribution*, not placement.
