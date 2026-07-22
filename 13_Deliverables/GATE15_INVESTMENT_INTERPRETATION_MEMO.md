# Investment Interpretation Memo — Oracle (ORCL)

Gate: 15 · Date: 2026-07-21, updated 2026-07-22 with research-prompt results
· Status: price triad still illustrative (Q-08/C-09 unresolved), but now
cross-checked against real market data; option-structure discussion now
uses real (rank-6) quotes. User-requested deadline: decide on a calls
position by end of week.

Companions: `12_Model/development/ORCL_8Q_Model_v0.6_Gate15_data_update.xlsx`
("Valuation (Gate 13)" §3b, "Sensitivities (Gate 14)" tabs),
`01_Research_Outputs/ORCL_User_Thesis_and_Questions.docx` (D-018),
`01_Research_Outputs/ORCL_Gemini_DeepResearch_Valuation_Data_2026-07-22.docx`
and `ORCL_ChatGPT_DeepResearch_Valuation_Data_2026-07-22.md` (SRC-025/026),
`decision_log.md` D-018/D-020/D-021/D-025/D-026/D-028,
`source_conflicts.md` C-12/C-13/C-14.

## 1. What changed since the first draft of this memo

The user ran this session's research prompt through Gemini Deep Research
and ChatGPT (2026-07-22). Both are **rank 6** (research-tool output) per
CLAUDE.md's source hierarchy — cross-checks, never controlling, and neither
was independently re-fetched from its cited primary source by this session
(SEC.gov returned a 403 to a direct fetch attempt). Within that limit:

- **Q-11 (preferred treatment) is now substantively resolved** (D-028): the
  Series D preferred mandatorily converts ~2029-01-15, after all four of
  this project's valuation dates — debt-like treatment, already used in the
  model, is structurally correct, not a placeholder.
- **Q-08 (real multiple) is still open**, but a useful cross-check exists:
  the two tools' peer EV/NTM EBITDA multiples disagree by 25-60% across
  every single peer (C-12) and are not usable. Oracle's own current
  market-implied EV/NTM EBITDA — 13.76x, a single-entity ratio not exposed
  to that peer-methodology mismatch — lands almost exactly on the
  illustrative Base case's 13.0x this memo already used. That is a genuine
  real-world signal that the illustrative Base assumption was reasonable,
  not proof of a "real" multiple for the model's four future valuation
  dates.
- **A real, important discrepancy surfaced in the options data (C-14):**
  Gemini's Black-Scholes-estimated premium for the Dec 2027 $150 call
  ($18-20) is roughly a third of ChatGPT's actual quoted market price for
  the same contract (~$61-70, bid/ask/last from Yahoo Finance). Trust the
  actual quote, not the model estimate, for anything 2027-dated. The two
  sources are much closer for 2026-dated strikes.

## 2. What the model says — illustrative price, now with a real cross-check

At the first valuation checkpoint (FY27 Q1 earnings, expected 2026-09-10),
the model's NTM window implies:

| Scenario | Illustrative multiple | Illustrative price |
|---|---|---|
| Bear | 10.0x EV/NTM EBITDA | ~$96/share |
| Base | 13.0x EV/NTM EBITDA | ~$166/share |
| Bull | 16.0x EV/NTM EBITDA | ~$244/share |

**Real cross-check:** ORCL's current share price is ~$126 (both tools agree
within ~1%, current as of 2026-07-22), against a current market-implied
EV/NTM EBITDA of 13.76x (Gemini) — i.e., **the market today is already
pricing Oracle close to this model's illustrative Base multiple**, on
today's NTM window. The stock is not at $166 today because today's NTM
EBITDA is smaller than the FY27-Q2-through-FY28-Q1 window this model's
"Base" price uses — the $166 figure is a forward target for September 2026,
not a claim that the stock is mispriced today. Your thesis is a bet that
either OCI growth tracks toward Base/Bull and/or the multiple itself
expands past 13x as execution derisks — both are still open questions the
Sept 2026 print will start to answer, not something today's data confirms
or refutes.

## 3. Instrument: stock vs. long calls vs. call spread — now with real IV data

Your thesis document (D-018) settled the instrument question — long calls,
full-premium downside tolerance. The new data adds a real consideration
worth taking seriously before finalizing structure, not before finalizing
instrument:

**Real volatility picture (rank 6, cross-checked between tools):**
- ORCL overall implied volatility: ~62.6% (75th percentile — elevated vs.
  its own history).
- Term structure by expiration (ATM IV): Sept 2026 ~71%, Dec 2026 ~69.5-70%,
  mid-late 2027 ~67-68%. IV is elevated everywhere but *highest* at the
  nearest (Sept 2026 earnings) expiration and gradually declines further out
  — a classic event-premium shape, not a flat surface.
- The Sept 18, 2026 straddle implies a ~23% move around that earnings
  release — a large expected swing, consistent with how binary this
  print could be for your thesis (a bad OCI/margin/leverage print could
  hit Bear-band levels fast; a strong one could re-rate quickly).

**What this means for long calls specifically:** buying a call with an
expiration close to Sept 2026 embeds paying near-peak IV, which decays
sharply (IV crush) right after the print regardless of which direction the
stock moves — a real cost your original instrument choice didn't have data
on. This doesn't overturn "long calls" as your instrument, but it is a real
reason to prefer:
- **An expiration past the immediate Sept 2026 event** (Dec 2026 or later)
  so you're not paying the single highest IV point on the term structure,
  and/or
- **Giving real weight to a call spread** for the specific leg that would
  otherwise carry the most IV-crush exposure, which is exactly the argument
  Gemini's analysis raised (buying $130 calls / selling $160 calls to
  neutralize Vega risk while still capturing OCI-driven upside). This is
  the first data-backed reason in this whole project to revisit your
  original spread-vs-calls answer — not a reason to reverse it, but a
  real trade-off you didn't have real numbers for when you first answered.

**Real premium reference points (Dec 18, 2026 expiration — cross-validated
between both tools, trustworthy per C-14):**

| Strike | Estimated/quoted premium | Source |
|---|---|---|
| $130 (near current $126 price) | ~$18-20 | Gemini B-S estimate ($18.20-$19.60) and ChatGPT actual quote (~$20.15, bid $19.80/ask $20.55) agree closely |
| $150 | ~$10-11 (Gemini estimate only; not independently quote-verified) | Gemini B-S estimate |
| $160 | ~$7-8 (Gemini estimate only) | Gemini B-S estimate |

**For any 2027-dated expiration, do not use Gemini's Black-Scholes table —
it materially underprices those contracts relative to the real quote
ChatGPT pulled (C-14).** Get a live quote from your own broker before
sizing a 2027 position; treat everything above as directional, not
executable, pricing.

## 4. Risk framing — unchanged, still holds

Your invalidation triggers (leverage stress, AI capex bust, margin
compression) map directly onto the ratified Bear case and the model's own
D-021 controls — see the prior version of this memo's §4 table, still
accurate. Nothing in the new data changes this mapping.

## 5. What's still genuinely open

- **The real EV/NTM EBITDA multiple (Q-08/C-09)** — the peer comps still
  disagree too much between tools to trust (C-12); the 13.76x market
  cross-check is useful but is today's multiple, not a sourced forecast
  multiple for September 2026 or later.
- **A verified, live options quote** — everything in §3 is rank 6 and, per
  C-14, partly unreliable for 2027 expirations. Pull your own broker's
  current quote for whatever strike/expiration you're actually considering
  before placing a trade.
- **The FY2030 OCI target disagreement (C-13, $100-120B vs. $166B)** —
  doesn't affect the near-term decision but is worth resolving if you want
  confidence in the multi-year thesis beyond this year's decision.

## 6. Bottom line

Long calls remain consistent with your thesis, risk tolerance, and holding
period. The new data sharpens — but doesn't reverse — that choice:
- The market's current ~13.76x multiple sitting near this model's Base case
  is a real, if imperfect, signal that your thesis isn't fighting an already
  euphoric price — there's room for the re-rating your thesis is betting on.
- The options market is pricing real, elevated event risk into the Sept
  2026 print (23% implied move, IV peaking right at that expiration) — this
  is a legitimate reason to consider an expiration past that date, or a
  spread structure for at least part of the position, rather than a reason
  to abandon calls.
- Get a live quote before sizing anything, especially at 2027 expirations,
  where the research-tool data itself disagrees by 3-4x (C-14).

If you decide before pulling a live quote, do so knowing this memo's price
triad is still illustrative and its options pricing is directional-only,
not executable.
