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
- Resolution source: FY26 10-K balance sheet + debt footnote — **now in repo as SRC-024**
  (`02_Annual_Filings/ORCL_2026_10-K_FY_Ended_2026-05-31.pdf`, registered 2026-07-20).
  Interim: FY26 Q4 earnings release / slides.
- *Gate 4 (2026-07-20):* designated resolution test = DEBT_030 computed from the FY26 10-K balance sheet (SRC-024); record whether the $135B claim included preferred/leases.
- **RESOLVED 2026-07-20 (Gate 5A pilot).** From SRC-024 balance sheet (PDF p.66) and
  Note 6 (p.85-86): notes payable and other borrowings current **$7,199M** +
  non-current **$122,342M** = **DEBT_030 = $129,541M** carrying value (gross principal
  $130,105M less $564M unamortized discount/issuance costs). The Framework's $129.5B
  is exactly Oracle's reported borrowings — **this is the model's gross-debt figure.**
  The Research Pack's "$135.0B" is best explained as borrowings + the $4,954M
  6.50% Series D Mandatory Convertible Preferred (= $134.5B, loosely rounded to $135B)
  — i.e., a *definitional* difference (preferred included), not a different date; the
  residual ~$0.5B is rank-6 rounding/estimation slop and is not reproducible from any
  filed figure. Convention adopted (pending Q-11/Q-13 for the EV bridge): gross debt =
  borrowings only; preferred ($4,954M), finance leases ($7,701M) and operating leases
  ($30,190M) tracked as separate components, never silently merged.
- **Gate 5B addendum (2026-07-20):** quarterly gross-debt series now populated for
  all eight quarters (FY25 Q1 $84,515M → FY25 Q4 $92,568M → FY26 Q1 $91,315M → FY26
  Q4 $129,541M), each tying exactly to DEBT_010+DEBT_020 on that period's own
  balance sheet. FY26 Q3 debt ($134,605M) is the peak quarter, just before the
  preferred issuance and subsequent paydown activity bring FY26 Q4 to $129,541M.

## C-02 — FY26 depreciation: ~$4.8B vs. ~$7.6B
- Research Pack quarterly depreciation rows sum to ~$4.78B for FY26 ($1,020+$1,100+$1,220+$1,438M).
- Framework: "FY26 depreciation increased to approximately $7.6 billion."
- Gap is large (~60%). Likely the Research Pack rows are a narrower definition (e.g., excluding amortization or lease depreciation) or simply estimated.
- Resolution source: FY26 10-K cash-flow statement and PP&E footnote — **now in repo as
  SRC-024**, registered 2026-07-20.
- *Gate 4 (2026-07-20):* designated resolution test = sum of standalone quarterly PROF_140 (YTD-differenced) vs. FY26 10-K annual depreciation (reconciliation plan §4).
- **RESOLVED 2026-07-20 (Gate 5A pilot).** FY2026 **depreciation = $7,623M**
  (SRC-024 cash-flow statement, PDF p.70; Note 4 PP&E states "$7.6 billion", p.83).
  This is depreciation ONLY (cash-flow add-back on PP&E, which per Note 4 includes
  finance-lease ROU assets); amortization of intangibles is a separate $1,671M line.
  The Framework's "~$7.6B" is therefore correct. The Research Pack's ~$4.78B quarterly
  series is an **unsupported estimate** (D-005/C-03 family) and is unusable. Designated
  quarterly tie verified in the pilot to the extent derivable: Q1 1,351 + (9M−Q1) 3,857
  + Q4 2,415 = 7,623 exactly (CHK-Q4-20); full four-quarter tie completes at Gate 5B.
  Model definition rule (D-014): depreciation (PROF_140) and amortization of
  intangibles are never combined without the explicit PROF_150/EBITDA formulas.
- **Gate 5B addendum (2026-07-20):** quarterly depreciation tie now closed for both
  fiscal years. FY25: 804+908+1,003+1,152=3,867 (10-K exact). FY26: 1,351+1,704+
  2,153+2,415=7,623 (10-K exact, CHKX-04). Depreciation roughly doubled quarter over
  quarter across FY26 as the AI-infrastructure buildout accelerated (Q1 $1,351M →
  Q4 $2,415M), consistent with the PP&E growth pattern (Note 4, FY26 10-K).

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
- Resolution source: FY26 10-K lease footnote — **now in repo as SRC-024**, registered
  2026-07-20.
- *Gate 4 (2026-07-20):* mapped to DEBT_070 (annual-only); press-sourced ~$260B remains unusable until the footnote value is extracted from SRC-024.
- **RESOLVED 2026-07-20 (Gate 5A pilot).** SRC-024 Note 9 (PDF p.92): "As of May 31,
  2026, we had **$260 billion** of additional lease commitments, substantially all
  related to data center arrangements, that are generally expected to **commence
  between the first quarter of fiscal 2027 and fiscal 2029** and for terms of
  **fifteen to nineteen years** that were **not reflected on our consolidated balance
  sheet** ... or in the maturities table." Includes a lease with a guarantee of up to
  **$3.3B** of the lessor's borrowing maturing September 2026. Characterization:
  (a) stated in whole billions, as-of 2026-05-31; (b) **excluded** from the reported
  operating/finance lease liabilities ($30,190M / $7,701M); (c) treatment decision —
  model as a **scheduled future commitment** (capacity build / committed-capital
  analysis, DEBT_070), **not** in current gross debt or net debt; it becomes debt-like
  only as leases commence and go on balance sheet. Related datapoints now primary:
  FY26 Q1 10-Q disclosed $99.8B (same footnote type), so the series is trackable
  quarterly; unconditional purchase obligations are separate ($13,309M, mostly data
  center power, + $19B post-year-end cloud-infrastructure commitments). The
  press-sourced ~$260B figure is superseded by the filed value.

## C-07 — RPO series: definitions and rounding
- Research Pack RPO series ($65B → $638B) is round-numbered and mixes points that Oracle disclosed with different emphasis (total RPO vs. cRPO). FY26 Q1 $455B, Q2 $523B, Q3 $553B, Q4 $638B need per-quarter verification against releases/10-Qs, including what share is current (~12% per Framework) and the ~$75B prepaid/BYOH claim.
- Resolution: extraction pass over the 8 earnings releases + 10-Qs; transcript language when transcripts are obtained.
- **RESOLVED 2026-07-20 (Gate 6).** Full eight-quarter RPO_010 series extracted
  directly from each period's 10-Q/10-K revenue-recognition footnote (rung 1–2,
  controlling) and cross-checked against every release headline (rung 3):
  FY25 Q1 $99.1B / Q2 $97.3B / Q3 $130.2B / Q4 $137.8B; FY26 Q1 $455.3B / Q2
  $523.3B / Q3 $552.6B / Q4 $638.0B. **All eight footnote values round exactly to
  their release headline** (e.g. Q3 FY26 footnote $552.6B → headline "$553
  billion"); no cross-document discrepancy found in any quarter. cRPO (RPO_030)
  recomputed as RPO_010 × RPO_020 for all eight quarters and labeled `calculated`
  per the reconciliation plan (FY25: $37.7B/$37.9B/$40.4B/$45.5B; FY26:
  $45.5B/$52.3B/$66.3B/$76.6B) — matches the Framework's implied ~10–12%
  current-RPO share for FY26 exactly (rungs 1–2 confirm rung-6 estimate was
  directionally right, but the filed % is now the controlling figure, not the
  Framework's narrative estimate). The Research Pack's round-numbered 12-quarter
  RPO series and its FY24 starting point ($65B) are **not** independently
  verified by this extraction (FY24 is out of the required FY25–FY26 scope per
  Q-03) and remain unusable pending an FY24 extension. The $75B prepaid/BYOH
  claim is separately confirmed from a primary source (FY26 Q4 release, "The
  prepaid and customer supplied hardware portions of our large AI contracts now
  total $75 billion") — see KPI_060 in the full extraction; this was a Gate 5A
  finding, reconfirmed here as consistent with no new conflict.

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

## C-12 — Peer EV/NTM EBITDA multiples disagree materially between Gemini and ChatGPT (2026-07-22)
- Both run by the user via `RESEARCH_PROMPT_FOR_EXTERNAL_AI.md` (Gate 15), same day, same peer set.
- ChatGPT (MarketScreener, FY2027 fiscal-year proxy): MSFT 12.09x, AMZN 9.99x, GOOGL 14.43x, SAP 10.05x, CRM 8.54x, IBM 11.54x.
- Gemini (provider not fully specified per-row, "Rolling 4-Qtr Calendar" NTM claimed): MSFT 15.71x, AMZN 16.27x, GOOGL 15.80x, SAP 15.40x, CRM 10.01x, IBM 14.72x.
- Gemini's multiples run ~25-60% higher than ChatGPT's across every single peer, which is too systematic to be random noise — likely a different NTM EBITDA definition/source, a different EV convention (e.g., Gemini may be including something ChatGPT excludes, or vice versa), or an error in one tool's arithmetic. Neither report shows its EBITDA calculation, so the gap can't be reconciled from repo holdings.
- Treatment: per D-021, this does not resolve Q-08/C-09. Neither multiple set is treated as "the" real peer multiple. The one point of usable signal is **Oracle's own current market-implied EV/NTM EBITDA**, computed by Gemini as 13.76x from Oracle's own current EV and its own NTM EBITDA consensus — a single-entity ratio, not a cross-peer comparison, so it isn't exposed to the same peer-to-peer methodology mismatch. Used as a market cross-check on the Valuation (Gate 13) tab, clearly labeled rank-6 and distinct from both the illustrative Framework multiple and a genuine sourced peer multiple.
- Resolution requires either a named, single, verifiable data provider queried directly (e.g., an authenticated FactSet session) or the user manually pulling each peer's own NTM EBITDA from a named terminal with a stated calculation methodology.

## C-13 — Oracle's FY2030 OCI revenue target: $100-120B vs. $166B
- Both AI reports agree on the FY2030 total-revenue ($225B) and non-GAAP EPS ($21.00) analyst-day targets (cross-checked, consistent).
- They disagree sharply on the FY2030 **OCI-specific** revenue target: Gemini reports "$100.0B-$120.0B" attributed to the Analyst Meeting presentation/RPO discussion; ChatGPT reports **$166 billion**, attributed to Reuters' contemporaneous coverage of the same October 16, 2025 meeting (an upward revision from an earlier-stated $144B path).
- Both cite the same event but different downstream sources (Oracle's own slide deck vs. Reuters' reporting on it) — this could reflect Gemini reading an older/different slide row, a transcription error, or Reuters reporting a figure not on the slides verbatim (e.g., a verbal statement by an executive).
- Treatment: unresolved. Neither figure is used in this model. If Q-05 (analyst-day materials) is ever obtained directly (the primary slide decks are publicly linked from Gemini's citation list — oracle.com/a/ocom/docs/corporate/financial-analyst-meeting-2025-*.pdf), pull the OCI FY30 number directly from the slide rather than trusting either research tool's transcription.

## C-14 — Gemini's Black-Scholes option-premium estimates vs. ChatGPT's actual quoted prices disagree sharply for long-dated calls
- ChatGPT reported **actual quoted market data** (bid/ask/last trade from Yahoo Finance) for the Dec 17, 2027 $150 call: last $61.00, bid $60.10, ask $63.75 (as of 2026-04-24), with a later delayed-quote snapshot of $70.08 (2026-07-22).
- Gemini reported a **self-labeled Black-Scholes estimate** ("Pricing Model / Source: Black-Scholes / OptionCharts") for the same instrument (Dec 17, 2027 $150 strike): $18.30-$20.00.
- These are not close — actual market price is roughly 3-4x Gemini's modeled estimate. For the nearer-dated Dec 18, 2026 $130 call, the two are much closer (Gemini's Black-Scholes range $18.20-$19.60 vs. ChatGPT's actual quote ~$20.15), so the estimate model is not uniformly bad — it appears to break down specifically for the longer-dated (2027) contracts, plausibly because a Black-Scholes estimate run without the real long-dated IV surface badly underprices LEAPS-style time value.
- **Treatment: for any 2027-expiration option, use ChatGPT's actual quoted bid/ask (or, better, a live broker quote) — do not use Gemini's Black-Scholes estimate table for long-dated strikes.** For near-dated (2026) strikes the two sources are close enough to cross-validate each other.
- This is exactly the kind of discrepancy this project's data-integrity rules exist to catch before it costs real money — an "estimated" premium presented without enough emphasis on the word "estimated" could otherwise be mistaken for a tradeable price.

## Confirmed consistencies (for the record)
Cross-checks that PASSED between the two AI reports (still requiring primary verification at Gate 6): FY26 capex $55.7B (quarterly sum matches); FY26 FCF −$23.7B (sum matches); FY26 year-end cash $31.3B; FY26 interest expense ~$4.6B (quarterly sum ≈ $4.64B); FY26 total revenue $67.4B; FY26 exit RPO $638B; FY27 guidance ($90B revenue, ~$70B net cash capex, ~$40B financing incl. $20B ATM).

**2026-07-22 (Gemini/ChatGPT deep-research reports, both rank 6, run via the
Gate 15 research prompt):** strong independent agreement on: ORCL current
share price (~$125.84-$127.05, ~1% spread, immaterial) and market cap
(~$360-366B); Series D mandatory convertible preferred terms (minimum/
maximum conversion rates 499.8126/624.7657 shares per preferred, initial
price ~$160.06, threshold appreciation price ~$200.07, mandatory conversion
date ~January 15, 2029) — precise numeric agreement between two
independently-run tools is a meaningful confidence signal even though
neither citation was independently fetched by this session (SEC.gov blocked
direct WebFetch, 403); FY2027 revenue guidance ~$90B and FY2027 non-GAAP EPS
guidance $8.05; FY2030 analyst-day targets of $225B total revenue and $21.00
non-GAAP EPS. Both reports agree the public web does not expose a clean,
named, terminal-style consensus for Oracle's non-GAAP EPS or OCI-growth/
capex by quarter — company guidance remains the best available figure for
those, consistent with Q-08's standing status.
