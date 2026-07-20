# EBITDA Definition Memo (Q-10)

Gate: 5A pilot · Date: 2026-07-20 · Status: **recommended — pending user sign-off (Gate 8 family)**
All figures below are FY2026 primary-source values extracted in the Gate 5A pilot
(sources: SRC-006, SRC-008, SRC-013, SRC-016, SRC-024; see pilot provenance file).

## 1. Why this matters

PROF_160 has been structurally blank since Gate 4 because "EBITDA" is ambiguous for
Oracle in FY26: depreciation tripled ($3.9B → $7.6B), SBC is large ($4.8B), FY26
non-operating income contains ~$2.8B of one-time investment gains (Ampere sale, Bloom
warrants), and $1.8B of restructuring hit operating income. The four candidate
definitions differ by **billions** — they are not interchangeable.

## 2. Candidate definitions evaluated (FY2026 actuals)

| # | Definition | Q1 FY26 | Q4 FY26 | FY2026 |
|---|---|---|---|---|
| 1 | GAAP operating income + depreciation (CF) + amortization of intangibles | 4,277+1,351+420 = **6,048** | 6,133+2,415+432 = **8,980** | 20,606+7,623+1,671 = **29,900** |
| 2 | GAAP net income + interest expense + taxes + D&A | 2,927+923+500+1,771 = **6,121** | 4,304+1,438+1,066+2,847 = **9,655** | 17,087+4,599+2,467+9,294 = **33,447** |
| 3 | Non-GAAP operating income + depreciation (CF) | 6,236+1,351 = **7,587** | 8,590+2,415 = **11,005** | 28,926+7,623 = **36,549** |
| 4 | #1 + restructuring/acquisition-related add-back | 6,048+415 = **6,463** | 8,980+823 = **9,803** | 29,900+1,838 = **31,738** |

Definition 2 exceeds definition 1 by exactly non-operating income, net (FY26: $3,547M,
of which $2,811M is investment gains) — i.e., a "net-income-up" EBITDA silently
capitalizes the one-time Ampere-type gains into the valuation metric. Definition 3
additionally adds back all SBC ($4,811M FY26). These are materially different numbers:
FY26 spread between #1 and #3 is $6.6B (~22%).

## 3. Recommendation

- **Primary model definition (PROF_160):** **Definition 1** —
  `EBITDA = GAAP operating income (PROF_010) + depreciation per cash-flow statement
  (PROF_140) + amortization of intangible assets (CF basis, = OPEX_040 line)`.
  Rationale: every component is a filed, auditable line; excludes non-operating items
  (so one-time investment gains never enter EBITDA); leaves SBC as a real expense;
  restructuring stays in (visible separately via OPEX_060/OPEX_065 for scenario
  adjustments).
- **Comparable-company definition (Gate 9):** the same construction applied to each
  peer's filed statements (operating income + D&A from their cash-flow statements),
  computed by us — never vendor "EBITDA" fields — so numerator and denominator of
  EV/EBITDA are built identically. If a peer multiple source can only provide
  SBC-added-back EBITDA, Oracle's metric must be recomputed on that basis for that
  comparison only, and labeled.
- **Non-GAAP cross-check definition:** Definition 3 (non-GAAP operating income +
  depreciation), used only to sanity-check consensus/vendor figures, which are usually
  closest to this basis. Never mixed into the primary series.
- **Valuation-adjusted secondary series:** Definition 4 ("adjusted EBITDA") = primary
  + restructuring and acquisition-related costs (OPEX_050/060/065). Kept as a separate
  calculated column at Gate 13 if needed; not the default.

## 4. Component treatments

| Item | Treatment in primary EBITDA | Rationale |
|---|---|---|
| Stock-based compensation | **Expense (not added back)** | $4.8B/yr recurring economic cost; adding back inflates EBITDA ~16% and biases EV/EBITDA vs. conservatively built peers. Cross-check series (#3) captures the SBC-out view. |
| Restructuring / acquisition-related | **In EBITDA (not added back)** | FY26 restructuring ($1.8B incl. up-to-$2.1B 2026 Plan) is cash and recurring in recent years; the adjusted series (#4) isolates it explicitly instead of hiding it. |
| Operating lease expense | **Expense (EBITDA, not EBITDAR)** | Operating lease cost ($2,794M FY26) stays in; consistent with leaving operating-lease liabilities out of gross debt (C-01 resolution). EV bridge and leverage must keep the same convention (Q-13). |
| Finance leases | Depreciation add-back includes finance-lease ROU amortization (finance-lease ROU assets sit inside PP&E per SRC-024 Note 4); interest on finance leases is below operating income anyway. FY26 finance-lease amortization $351M — flagged, not separable from the CF depreciation line. |
| Amortization of intangibles | **Added back** (it is the "A") | Filed line, non-cash, acquisition-driven. |
| One-time gains (Ampere, Bloom) | **Never in EBITDA** under definition 1 (non-operating) | This is the decisive argument against a net-income-up build (#2). |
| Interest income | Not in EBITDA (non-operating). |

## 5. Limitations and reconciliation requirements

1. Quarterly depreciation is only available via YTD differencing of cash-flow
   statements (Q4 = FY − 9M); each quarterly PROF_160 inherits that derivation and is
   classified `calculated`.
2. The CF depreciation line is not identical to a pure "PP&E depreciation expense by
   function" disclosure; Oracle's Note 4 confirms $7.6B FY26, so drift is currently nil,
   but the tie must be re-checked each year (CHECK_060 family).
3. Sum-of-quarters EBITDA must reconcile to annual EBITDA (CHECK_050) once all four
   quarters are extracted at Gate 5B.
4. Any peer comparison must state which definition (#1/#3/#4) is in use; mixed-basis
   multiples are prohibited (extends precedence rule 3 on GAAP/non-GAAP separation).
5. This memo does **not** close the lease-convention question for EV (Q-13) or the
   preferred treatment (Q-11); it only fixes the EBITDA numerator convention.

## 6. Status

Logged as **D-014 (provisional)**. PROF_160 is populated in the pilot under
definition 1 and labeled `calculated / provisional pending user sign-off`. Q-10 moves
to "recommendation issued — awaiting user ratification"; per Gate 4 review §10(f), the
user approves, the analyst proposes.
