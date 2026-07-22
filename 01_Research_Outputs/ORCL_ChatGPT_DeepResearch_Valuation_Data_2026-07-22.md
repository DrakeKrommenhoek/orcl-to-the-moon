# Oracle valuation model sourcebook (ChatGPT deep research output)

Pasted verbatim from ChatGPT into this session on 2026-07-22, in response to
the research prompt at `11_Analysis/valuation/RESEARCH_PROMPT_FOR_EXTERNAL_AI.md`.
Rank 6 source (research-tool output) per CLAUDE.md's source-authority
hierarchy — cross-check only, never controlling. See `source_conflicts.md`
for disagreements between this and the companion Gemini report
(`ORCL_Gemini_DeepResearch_Valuation_Data_2026-07-22.docx`).

---

I prioritized primary sources first, then named market-data providers. Where a clean, current, named source was not publicly extractable in this environment, I say so explicitly rather than guess. All money figures below are in the source currency shown by the cited provider unless noted otherwise.

## Oracle current market data

Section 1.

| Item | Value | Source | As-of date |
|---|---:|---|---|
| ORCL current share price | **$125.84** regular-session close; the same source also showed **$126.35** after-hours | TradingView ORCL quote page and Stocktwits ORCL snapshot. | **2026-07-22** |
| ORCL current market cap | **$365.96 billion** | TradingView / Stocktwits ORCL quote pages. | **2026-07-22** |
| Oracle cash and marketable securities | **$31.894 billion** | Oracle FY2026 Q4 earnings press release PDF, balance-sheet snapshot. | **2026-05-31** |
| Oracle notes payable and other borrowings | **$129.541 billion** | Oracle FY2026 Q4 earnings press release PDF, balance-sheet snapshot. | **2026-05-31** |
| Series D mandatory convertible preferred stock | **$5.0 billion gross issued** | Oracle Series D preferred prospectus supplement and Oracle FY2026 Q4 cash-flow statement. | **2026-02-05 issuance; 2026-05-31 cash-flow disclosure** |
| Oracle enterprise value | **Approximately $468.6 billion**, using current market cap plus debt plus Series D preferred minus cash/marketable securities | Self-calculation from current market cap and Oracle FY2026 Q4 balance-sheet / financing disclosures. | **Market cap: 2026-07-22; net debt inputs: 2026-05-31** |
| Current implied common shares outstanding | **Approximately 2.91 billion shares**, computed as market cap divided by share price | Self-calculation. Market-data implied share count, not a statutory SEC cover-page share count. | **2026-07-22** |

ATM: Feb 1, 2026 financing plan authorized up to $20B ATM common-equity program. June 10, 2026: FY2027 funding expected ~$40B debt and equity, including the $20B ATM. No post-June 10, 2026 SEC filing or IR release found quantifying completed ATM sales or post-June buybacks through 2026-07-22.

## Oracle options market

Section 2.

| Item | Value | Source | As-of date |
|---|---:|---|---|
| ORCL overall implied volatility | **62.6%** IV, **75th percentile** | Market Chameleon ORCL IV page. | **2026-07-22** |
| Sep 18, 2026 $130 call | Last $28.37 (stale snippet); bid/ask $0.00; volume 2; OI 0 | Yahoo Finance options-chain snippet — clearly stale/low-quality. | **Last trade shown 2026-04-07** |
| Dec 18, 2026 $130 call | Last $20.15; bid $19.80; ask $20.55; volume 128; OI 801; IV **69.85%** | Yahoo Finance Australia options-chain snippet. | **2026-07-16** |
| Dec 17, 2027 $150 call | Last $61.00; bid $60.10; ask $63.75; volume 11; OI 205; IV **61.41%** | Yahoo Finance options-chain snippet. | **2026-04-24** |
| Dec 17, 2027 $150 call (later snapshot) | $70.08 delayed quote | Yahoo Finance quote page. | **2026-07-22 9:46 AM EDT** |
| Dec 17, 2027 $180 call | $87.15 delayed quote | Yahoo Finance quote/chart page. | **2026-07-22** |

Only cleanly-verified strike-level IV: Dec 18, 2026 $130 call at 69.85% IV, above the 62.6% stock-level IV snapshot — consistent with event premium into the next earnings cycle. OI concentration: 801 contracts at Dec 2026 $130 call, 205 at Dec 2027 $150 call. Could not verify a full skew surface or unusual-volume leaderboard without terminal-grade access.

## Peer comparable-company market data

Section 3. Caveat: fiscal-year-based forecast windows, not a true common calendar-quarter NTM roll for every company (source: MarketScreener).

| Company | Share price | Market cap | EV | Fcst revenue | Fcst EBITDA | Fcst EPS | EV/EBITDA | P/EPS | Window | As-of |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|---|
| Microsoft | $397.75 | $2,954,660m | $2,898,461m | $384,874m | $239,800m | $19.51 | 12.09x | 20.39x | FY2027 (close proxy for NTM) | 2026-07-22 |
| Amazon | $247.55 | $2,662,922m | $2,635,067m | $931,258m | $263,780m | $9.903 | 9.99x | 25.00x | FY2027, not calendar NTM | 2026-07-22 |
| Alphabet | $342.09 | $4,230,960m | $4,148,688m | $586,473m | $287,573m | $14.71 | 14.43x | 23.26x | FY2027, not calendar NTM | 2026-07-22 |
| SAP | €132.04 | €153,301m | €149,605m | €44,865m | €14,888m | €8.13 | 10.05x | 16.24x | FY2027, not calendar NTM | 2026-07-22 |
| Salesforce | $170.06 | $139,279m | $165,169m | $50,514m | $19,336m | $9.563 | 8.54x | 17.78x | FY2028 needed for full NTM; not used | 2026-07-22 |
| IBM | $210.50 | $197,846m | $243,174m | $73,437m | $21,072m | $10.97 | 11.54x | 19.19x | FY2027, not calendar NTM | 2026-07-22 |

Source: MarketScreener valuation pages. Names most needing calendarization: AMZN, GOOGL, IBM, SAP, CRM.

## Oracle institutional consensus

Section 4.

FY2027 revenue: $89.317B (MarketScreener). FY2028 revenue: $130.470B (MarketScreener). FY2027 GAAP EPS: $6.435. FY2028 GAAP EPS: $8.937 (MarketScreener). Current-quarter EPS estimate: $1.73; current FY estimate: $8.05; next FY estimate: $10.91 (MarketWatch, basis unspecified). Company guidance (2026-06-10, not consensus): FY27 Q1 total revenue +27% to +29%; total cloud revenue +58% to +64%; FY27 non-GAAP EPS guide $8.05; FY27 net cash capex ~$70B; customer prepayment/timing impacts $20-25B. CreditSights (single-firm, 2026-04): FY27 capex $67.5B, FY28 capex $85B.

Bottom line: public sources support FY27/FY28 revenue and GAAP EPS, plus FY27 quarterly revenue/EBITDA, but NOT a clean public non-GAAP EPS consensus or OCI-growth/capex consensus pack — those remain company guidance or single-firm views, not a terminal-style consensus feed.

## Oracle mandatory convertible preferred stock

Section 5.

6.50% Series D Mandatory Convertible Preferred Stock (ORCL-PRD), Oracle 424B5/8-A/8-K, 2026-02-05. 100,000,000 depositary shares (1/2,000th of one preferred share each); 50,000 preferred shares issued. Liquidation preference $100,000/preferred share ($50/depositary share). Dividend rate 6.50%. Mandatory conversion range 499.8126 to 624.7657 common shares per preferred share, subject to anti-dilution adjustments. Initial price ~$160.06. Threshold appreciation price ~$200.07. Automatic conversion on the second business day after the final averaging period, defined off January 15, 2029. Optional early conversion before Jan 15, 2029 at the minimum conversion rate (499.8126). Fundamental-change conversion rate adjustment and make-whole dividend amount, with Oracle's right to settle in common stock. Anti-dilution adjustments cover rights/warrants offerings and stock splits/combinations. Diluted EPS treatment not spelled out in a one-line policy in the filings reviewed — inferred as an if-converted-style analysis given the mandatory 2029 settlement and holder optional-conversion right, not a company-quoted accounting policy.

## New items since the FY2026 Q4 release

Section 6.

No post-June 10, 2026 Oracle IR guidance update found through 2026-07-22. Reuters: AI capex pressuring Big Tech FCF; Oracle plans up to $50B debt/equity financing amid negative FCF (2026-07-22). Financial Times: Oracle could face a $7B collateral bill tied to the Wisconsin data-center project (2026-07-21). Barchart (secondary, unverified at agency level): S&P downgraded Oracle to BBB- from BBB. No post-June-10 debt-issuance press release/filing found.

Transcript-backed commentary (Oracle FY2025 Q1 - FY2026 Q4 calls): Q4 GPU utilization 97.5% globally (2026-06-10); FY26 Q2 (2025-12-10) customers can bring their own chips, some vendors rent capacity rather than sell it, synchronizing payments with receipts; FY26 Q4 net cash capex ~$70B excluding $20-25B customer prepayments/timing; CFO said infrastructure business generates steady-state ROIC in the high 20s; FY26 Q3 (2026-03-10) >10 GW of power/data capacity secured, >90% funded through partners; FY26 Q3 OCI gross margin on delivered AI capacity >30%, at 32%; FY25 Q1/FY26 Q2 demand outstripping supply, handed over ~400 MW in a quarter, 50% more GPU capacity than prior quarter; FY26 Q4 Oracle Health: 14 VA medical centers, 29,000 clinicians, 500,000 veterans; FY25 Q1 Ellison: "all of Cerner is the monetization" (AI embedded in health workflows, not sold separately). No explicit Oracle Health segment-profitability target or operating margin found in the transcripts reviewed.

## Oracle Financial Analyst Meeting (2025-10-16)

Section 7.

Oracle IR archives the event with slides and replay. Financial-outlook slides: total revenue $57B FY25, $67B FY26E, $85B FY27E, $130B FY28E, $185B FY29E, $225B FY30E (~31% CAGR). Non-GAAP EPS $6.03 FY25, $6.85 FY26E, $8.00 FY27E, $10.65 FY28E, $16.00 FY29E, $21.00 FY30E (~28% CAGR). OCI revenue target preview (2025-09-09 Q1 FY26 release): $18B FY26, then $32B/$73B/$114B/$144B over the following four fiscal years. Reuters coverage of the analyst meeting (2025-10-16): Oracle now expects OCI revenue to reach **$166 billion in FY2030**, above the earlier $144B path. Slides say Oracle intends to pursue customers based on profit potential, use diverse financing options to scale faster, and match expenses with revenue for datacenter builds.
