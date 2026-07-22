# External Research Prompt — for Gemini Deep Research / ChatGPT / Perplexity

Purpose: unblock Q-08 (consensus/market-data source) and C-09 (stale comp
table) for Gate 13's real multiple assignment, plus a few smaller open
items, ahead of a stock-vs-options decision targeted for end of week.

Paste the block below into the external tool. Everything it returns should
be treated as rank-6 (research-tool output) per this project's source
hierarchy — usable to fill the model's blocked cells only if every figure
carries a specific source and an as-of date; anything without one stays
unusable, same as the AI research packs already in this project.

---

## Prompt to paste

I'm building an institutional-quality valuation model for Oracle (ORCL) and
need current, precisely-sourced data to complete it. For every data point
below, cite the specific source (filing, press release, data provider) and
the exact as-of date. Do not give me a single blended "consensus" number
without naming where it came from — I need to know if it's from Bloomberg,
FactSet, Visible Alpha, Yahoo Finance, TIKR, or something else, and when it
was pulled, because stale or unsourced numbers are unusable for this model.

**1. Oracle current market data**
- Current ORCL share price, market cap, and enterprise value, with the
  exact as-of date/time.
- Current shares outstanding (basic) and any recent (since June 2026) ATM
  common-stock issuance activity or share buybacks.

**2. Oracle options market (for a stock-vs-calls-vs-call-spread decision)**
- Current implied volatility for ORCL options, by expiration, especially
  expirations near September 2026 (next earnings), December 2026, and
  mid-to-late 2027.
- At-the-money and slightly-out-of-the-money call prices/premiums for
  those expirations, with strikes bracketing $110-$180.
- Any notable options-market skew or unusual volume/open-interest
  concentration in ORCL calls, and the source/date.

**3. Peer comparable-company market data** (needed for EV/NTM EBITDA and
P/NTM EPS multiples) — for Microsoft (MSFT), Amazon (AMZN), Alphabet
(GOOGL), SAP, Salesforce (CRM), and IBM:
- Current share price, market cap, enterprise value (as-of date required).
- NTM (next-twelve-months) consensus revenue, EBITDA, and EPS estimates,
  with the provider named.
- Resulting implied EV/NTM EBITDA and P/NTM EPS multiples for each.
- Note: I need to align these to a common calendar-quarter NTM window
  across companies with different fiscal year ends (Oracle FYE 5/31,
  Microsoft FYE 6/30, Amazon/Alphabet/IBM/SAP FYE 12/31, Salesforce FYE
  1/31) — flag if your source's NTM window is fiscal-year-based instead of
  calendar-based so I can adjust.

**4. Oracle institutional consensus** (for FY2027 and FY2028, by quarter if
available, otherwise annual): revenue, non-GAAP EPS, GAAP EPS, OCI/cloud
infrastructure growth rate expectations, capex expectations. Name the
source (Bloomberg/FactSet/Visible Alpha/other) and as-of date for each.

**5. Oracle mandatory convertible preferred stock** (issued ~FY2026, $5
billion, "6.50% Series D Mandatory Convertible Preferred"): find the
Certificate of Designations or prospectus supplement and report the
conversion ratio (or conversion price range), the mandatory conversion
date, any anti-dilution or make-whole provisions, and how it's expected to
be treated in Oracle's diluted EPS calculation. Cite the SEC filing
(8-A, 8-K, or prospectus supplement) directly.

**6. Anything new since Oracle's FY2026 Q4 earnings release (June 10,
2026)**: FY2027 Q1 guidance updates or pre-announcements, analyst
commentary on OCI margins/utilization/customer funding, credit rating
actions (Moody's/S&P/Fitch), new debt issuance, and any Oracle earnings
call transcript commentary (FY2025 Q1 through FY2026 Q4) on: utilization
ramp for new AI infrastructure capacity, customer-supplied-hardware
accounting treatment, sustainable capex level after the current buildout,
and Oracle Health segment profitability. Cite transcript source and date
for each.

**7. Oracle's October 16, 2025 Financial Analyst Meeting**: any available
summary, slides, or transcript covering long-term targets (including any
FY2030 OCI revenue target), and cite the source.

Please organize your answer by these seven numbered sections, and inside
each one, give me a simple table or list with a Value / Source / As-of-date
column structure wherever possible, so I can drop the sourced figures
directly into a spreadsheet.

---

## What this unblocks in the model

Section 1 → current price for the eventual stock-vs-options comparison.
Section 2 → the actual options decision (strike/expiration/structure).
Section 3 → Gate 13's real EV/NTM EBITDA and P/NTM EPS multiples (currently
blank, yellow-highlighted, on the "Valuation (Gate 13)" tab) — this is the
single biggest unblock, resolving Q-08/C-09.
Section 4 → cross-checks the model's own bottom-up forecast against what
the market already expects (Framework Sec11's own stated need).
Section 5 → resolves Q-11 (preferred treatment), sharpening the EPS/equity
bridge.
Section 6-7 → resolves Q-04/Q-05 (transcripts/analyst day), the last open
qualitative-research items.
