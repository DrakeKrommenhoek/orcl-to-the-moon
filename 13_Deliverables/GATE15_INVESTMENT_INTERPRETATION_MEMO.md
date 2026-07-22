# Investment Interpretation Memo — Oracle (ORCL)

Gate: 15 · Date: 2026-07-21 · Status: **built on the illustrative multiple**
(Q-08/C-09 unresolved — see caveat in every section). User-requested
deadline: decide on a calls position by end of week (2026-07-21 week).

Companions: `12_Model/development/ORCL_8Q_Model_v0.5_Gate14.xlsx`
("Sensitivities (Gate 14)" tab), `01_Research_Outputs/
ORCL_User_Thesis_and_Questions.docx` (D-018), `decision_log.md` D-018/D-020/
D-021/D-025/D-026, `11_Analysis/valuation/RESEARCH_PROMPT_FOR_EXTERNAL_AI.md`
(sent this session — its output should refine this memo before acting).

## 1. The one caveat that governs this whole memo

**Every price figure below is illustrative, not sourced.** It uses the
Framework's own explicitly-unadopted candidate EV/NTM EBITDA multiples
(Bear 10x / Base 13x / Bull 16x), not a real, as-of-dated peer multiple —
Q-08 (no authenticated consensus/market-data source) and C-09 (stale,
single-sourced comp table) are still open. If the external research prompt
sent this session comes back with real peer multiples and current market
data before you decide, **redo the Gate 13/14 illustrative cells with real
numbers first** — the mechanism is built and ready to receive them; only the
inputs are placeholders. Treat everything quantitative in this memo as a
structural rehearsal of the decision, not the decision's actual inputs.

## 2. What the model says (illustrative)

At the first valuation checkpoint (FY27 Q1 earnings, expected 2026-09-10 —
about 7 weeks from today), the model's NTM window (FY27 Q2 through FY28 Q1)
implies:

| Scenario | Illustrative multiple | Illustrative price |
|---|---|---|
| Bear | 10.0x EV/NTM EBITDA | ~$96/share |
| Base | 13.0x EV/NTM EBITDA | ~$166/share |
| Bull | 16.0x EV/NTM EBITDA | ~$244/share |

Important framing: this is a **forward target as of the September 2026
earnings date**, not an assessment of today's fair value — the NTM window
starts the quarter *after* that release. Between now and then, the stock
trades on anticipation of that release and on the broader AI-infrastructure
narrative, not on this model's specific mechanics.

Your stated thesis ($150 within 2-3 quarters if not by year-end 2026, via
multiple expansion) sits **between the Base and Bull illustrative cases** —
closer to Base, but requiring some combination of (a) OCI growth executing
at or above the Base range (112-118% FY27), and/or (b) the market awarding
something above a 13x multiple before fundamentals fully justify it (i.e.,
real multiple expansion, which is exactly what your thesis names as the
mechanism). This is a coherent, not contradictory, reading of your own
thesis against the model — it does not require the Bull operating case to
be right, just a multiple modestly above Base's illustrative 13x, or Base
fundamentals with early credit for improving trajectory.

## 3. Instrument: stock vs. long calls vs. call spread

Your thesis document (D-018) already settled the instrument question —
**long calls**, with full-premium downside tolerance. This section checks
that choice against what the model shows, rather than re-opening it.

**Why long calls fit this specific setup better than stock, given your own
answers:**
- Your downside tolerance is explicit and total (100% of premium) — a
  position sizing choice, not a risk-management gap. Calls cap your dollar
  loss at the premium regardless of how far Bear plays out, which stock
  ownership does not.
- Your 6-18 month window comfortably covers the first (Sept 2026) and
  likely the second (est. Dec 2026) valuation checkpoints — enough time for
  the "multiple expansion" thesis to play out across more than one earnings
  print, which matters because a single quarter rarely re-rates a stock on
  its own (Framework §12's milestone list is explicitly about a *pattern*
  of confirmations, not one data point).
- The bear/base/bull spread here (~$96 to ~$244, illustrative) is wide
  enough that leverage via calls meaningfully amplifies the base-to-bull
  move your thesis is betting on, which is the point of choosing options
  over stock in the first place.

**Why NOT a call spread, given your own answers:** a call spread caps your
upside in exchange for cheaper premium — that trade only makes sense if you
have a *view on the ceiling* (you expect Base or a mild Bull, not more). Your
stated thesis is unambiguously bullish with an explicit multiple-expansion
mechanism and no stated cap; if you genuinely believe more than modest
upside is on the table, capping it via a spread works against your own
stated view. A spread would be the better structure only if you want to
reduce cost/breakeven at the expense of the tail — worth asking yourself
directly, but it's a change from what you already told me, not a
consequence of anything the model found.

**Structural decision I cannot make for you (needs the research-prompt
output, section 2):** strike and expiration. Two things determine this, and
neither is in the model yet:
1. **Expiration** should extend past your target catalyst window — likely
   past the Sept 2026 print, and probably past the Dec 2026 one too, given
   Framework §12's point that a single quarter rarely re-rates a stock.
   Given your "2-3 quarters, or by EOY 2026" framing, an expiration in the
   Dec 2026-Mar 2027 range is a reasonable starting point to discuss once
   real premium/IV data is in hand, not a number I'm asserting here.
2. **Strike** should be chosen against the actual current share price and
   the actual current implied volatility surface, both of which are exactly
   what the research prompt's Section 1-2 asks for. Choosing a strike
   without that data would be fabricating a market input this project's
   rules prohibit.

## 4. Risk framing — your invalidation triggers against the model's own scenario logic

Your stated invalidation triggers (D-018) map directly onto the ratified
Bear case (D-020) and the model's own controls (D-021), which is worth
noting explicitly — the project's risk framework and your personal risk
framework are already the same thing, not two things to reconcile:

| Your trigger | Where it shows up in the model |
|---|---|
| Balance-sheet/leverage stress | Bear case: ending gross debt $155-165B (FY27) vs. Base $145-153B; Cash Flow & Returns tab's lease-adjusted net leverage control (D-021) — Base-case illustrative leverage runs ~5.4x FY27 improving to ~4.8x FY28; a Bear case would show this stalling or rising instead of improving |
| AI capex bust | Bear case: OCI growth 88-98%/50-65% (FY27/28) vs. Base 112-118%/85-100% — a sharp OCI deceleration is literally the bear scenario's defining feature |
| Margin compression | Bear case: GAAP gross margin 53-56%/50-54% vs. Base 55-58%/52-57%; the model's own EBITDA-less-capex and FCF controls (Cash Flow & Returns tab) would show deterioration first, before it shows up in a headline miss |

Practically: if the Sept 2026 print shows OCI growth tracking toward the
Bear band, gross margin compressing toward the Bear band, or debt/leverage
guidance worsening rather than the Base case's expected "leverage peaks then
declines" pattern — that is your exit signal, consistent with what you told
me before any of this modeling happened, not a new conclusion the model
forced on you.

## 5. What would change this memo's conclusion

- **A real multiple (Q-08/C-09).** If peer multiples come back meaningfully
  below the Framework's illustrative 12-14x Base range, the whole price
  triad shifts down and the calls decision should be revisited before, not
  after, sizing a position.
- **Current option prices/IV (research prompt §2).** High implied
  volatility on ORCL calls right now would make the "long calls" structure
  more expensive to express the same view — worth checking before
  committing capital, since your thesis chose the instrument but the market
  sets the price of expressing it.
- **The mandatory convertible's actual terms (Q-11).** If conversion is
  imminent or highly dilutive, the EPS/equity bridge this memo's price
  triad rests on shifts — this is exactly why Gate 13 flagged Q-11 as an
  unresolved dependency rather than silently picking a treatment and moving
  on.

## 6. Bottom line

Your instrument choice (long calls) is internally consistent with your own
stated thesis, risk tolerance, and holding period — nothing in the model
argues against it, and the illustrative bear/base/bull spread is wide enough
to justify leverage over outright stock ownership. What remains before
actually placing a trade is not a modeling question but a **data question**:
real peer multiples, real current option prices, and the preferred's actual
terms — all three requested in this session's research prompt. If you get
that data back before end of week, bring it here and I'll fold it into Gate
13/14 and re-run this memo's numbers properly; if you decide before that
data arrives, do so knowing the price triad above is a structural rehearsal,
not a sourced forecast.
