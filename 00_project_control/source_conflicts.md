# Source Conflicts and Data-Integrity Flags

Date opened: 2026-07-20
Status: OPEN — none of these are resolved yet. Resolution happens at Gates 5–6
(extraction and reconciliation) against primary filings. Do not use conflicted figures
in the model until the winning source is recorded here with a citation.

Naming: "Research Pack" = `01_Research_Outputs/ORCL_Public_Markets_Research_Pack_2026-07-20.docx`.
"Framework" = `01_Research_Outputs/ORCL_Eight_Quarter_Model_Framework_2026-07-20.docx`.

## C-01 — FY26 year-end gross debt: $135B vs. $129.5B
- Research Pack (§1.2 and §3.5): gross debt $135.0B at FY26 year end.
- Framework (§5 balance-sheet table): current borrowings $7.2B + noncurrent $122.3B = **$129.5B** gross debt.
- Gap: ~$5.5B. Possible causes: inclusion/exclusion of the ~$5B mandatory convertible preferred, finance leases, or estimate error.
- Resolution source: FY26 10-K balance sheet + debt footnote (**not yet in repo**). Interim: FY26 Q4 earnings release / slides.

## C-02 — FY26 depreciation: ~$4.8B vs. ~$7.6B
- Research Pack quarterly depreciation rows sum to ~$4.78B for FY26 ($1,020+$1,100+$1,220+$1,438M).
- Framework: "FY26 depreciation increased to approximately $7.6 billion."
- Gap is large (~60%). Likely the Research Pack rows are a narrower definition (e.g., excluding amortization or lease depreciation) or simply estimated.
- Resolution source: FY26 10-K cash-flow statement and PP&E footnote.

## C-03 — Research Pack quarterly OCI and SaaS revenue splits are suspiciously round
- Every OCI quarterly figure FY24 Q1–FY26 Q4 is a round hundred ($1,500, $1,600, … $5,800M); SaaS likewise.
- Oracle historically disclosed OCI/SaaS growth rates and selected dollar figures, not a clean quarterly dollar series for 12 quarters. These rows are almost certainly **estimates presented without an estimate label**.
- Framework independently states FY26 OCI = $18.1B; Research Pack FY26 OCI rows sum to $18.1B — consistent, but both may share an estimation lineage.
- Treatment: classify entire OCI/SaaS quarterly split in the Research Pack as *research estimates*; rebuild the split from filings, earnings releases, slides, and call transcripts during extraction.

## C-04 — Research Pack FY26 revenue-line reclassification rows look internally inconsistent
- FY26 rows for "Cloud Svc & Lic. Supp." ($7,186*, $8,000*, $8,900*, $9,913*) and "Cloud & On-Prem Lic." ($5,700*, $5,900*, $6,100*, $6,800*) are marked * for a "reporting reclassification" (Total Cloud vs. Software split).
- Problems: (a) the two FY26 row labels no longer mean what the FY24–25 rows mean, making the table discontinuous; (b) FY26 "license" magnitudes ($5.7–6.8B/qtr) contradict the Framework's FY26 software-license revenue of **$4.7B for the full year**; (c) sub-rows no longer sum to the parent rows.
- Treatment: do not extract any FY26 revenue-line detail from the Research Pack. Use 10-Q/10-K category tables and rebuild a consistent six-stream recast (OCI, cloud apps, support, license, hardware, services) per the Framework architecture.

## C-05 — FY26 financing activity: multiple non-identical descriptions
- Research Pack §3.5: FY26 raised "$43B in debt and $5B in equity"; §2 (Q3 FY26): "$50B total capital raise plan ($30B debt/convertibles executed in Q3)."
- Framework §5: "$5B mandatory convertible preferred" + "up to $20B common-stock ATM" authorized; FY27 plan ~$40B.
- Financing Plan PDF (2026-02-01) is in the repo but its contents have not yet been extracted and reconciled.
- Resolution: extract the Financing Plan announcement, FY26 10-K financing-activities section, and the 8-A/prospectus for the mandatory convertible (URL in Framework source list).

## C-06 — ~$260B uncommenced operating-lease commitments is press-sourced, unverified
- Framework §5 cites "a financial-publication review" (investors.com) for ~$260B of leases signed but not yet commenced, and itself says the exact 10-K footnote must be verified.
- This number materially affects committed-capital and lease-adjusted leverage analysis.
- Resolution source: FY26 10-K lease footnote (**not yet in repo**).

## C-07 — RPO series: definitions and rounding
- Research Pack RPO series ($65B → $638B) is round-numbered and mixes points that Oracle disclosed with different emphasis (total RPO vs. cRPO). FY26 Q1 $455B, Q2 $523B, Q3 $553B, Q4 $638B need per-quarter verification against releases/10-Qs, including what share is current (~12% per Framework) and the ~$75B prepaid/BYOH claim.
- Resolution: extraction pass over the 8 earnings releases + 10-Qs; transcript language when transcripts are obtained.

## C-08 — GAAP vs. non-GAAP labeling risk in Research Pack aggregates
- Research Pack quarterly GAAP/non-GAAP operating income, margins, and "Calculated EBITDA" are not tied to a stated reconciliation. EBITDA rows imply D&A ≈ the (suspect) depreciation rows in C-02.
- Treatment: never source margin or EBITDA history from the Research Pack; compute from filings with an explicit documented EBITDA definition (see open question Q-10).

## C-09 — Comparable-company market data is single-sourced and time-boxed
- The entire comp table (prices, market caps, EV, NTM estimates, multiples; as-of 2026-07-17/20) exists only in the Research Pack, citing TIKR/FactSet/S&P without row-level attribution. NTM estimates are consensus-like data with no visible provider.
- Both AI reports agree that CoreWeave is reference-only, but they disagree in emphasis on Amazon/Alphabet (Research Pack: "weak valuation comps"; Framework: primary OCI comparables). Peer-set weighting is a Gate 9 methodology decision.
- Treatment: comp table is illustrative only. Re-source market data with explicit as-of dates before Gate 9/13.

## C-10 — Fiscal-period alignment between Oracle and peers
- Oracle FYE 5/31; Microsoft FYE 6/30; peers 12/31 (AMZN, GOOGL, IBM, SAP) and 1/31 (CRM, NOW have 12/31 and 1/31 respectively). NTM metrics mitigate this but require consistent NTM window construction. No convention has been chosen yet (open question Q-12).

## C-11 — FY27 Q1 EPS guidance vs. consensus framing
- Research Pack §2: Q1 FY27 non-GAAP EPS guide "$1.72–$1.76 vs $1.85 consensus" and FY27 EPS $8.05; Framework repeats $8.05 and $1.72–$1.76. The $1.85 consensus figure is unattributed and unverifiable from repo holdings.
- Treatment: classify $8.05 and $1.72–$1.76 as management guidance pending transcript/release verification; classify $1.85 as unverified consensus.

## Confirmed consistencies (for the record)
Cross-checks that PASSED between the two AI reports (still requiring primary verification at Gate 6): FY26 capex $55.7B (quarterly sum matches); FY26 FCF −$23.7B (sum matches); FY26 year-end cash $31.3B; FY26 interest expense ~$4.6B (quarterly sum ≈ $4.64B); FY26 total revenue $67.4B; FY26 exit RPO $638B; FY27 guidance ($90B revenue, ~$70B net cash capex, ~$40B financing incl. $20B ATM).
