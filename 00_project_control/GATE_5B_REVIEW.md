# Gate 5B Review — Full Historical Extraction

Date: 2026-07-20 · Session scope: FY2025 Q1 – FY2026 Q4 (all eight quarters) plus
both fiscal-year annual anchors, extending the Gate 5A pilot per its exact next
prompt. Branch: `claude/oracle-historical-extraction-pilot-r6o3ov`.

## 1. Scope

Full eight-quarter historical extraction: FY2025 Q1–Q4 (pre-FY26 statement
captions) and FY2026 Q1–Q4 (D-013 dual-presentation captions), following the same
methodology validated in Gate 5A — direct extraction where 10-Qs/releases disclose
a standalone quarter, YTD differencing where only cumulative figures exist, and
FY-minus-nine-month derivation for both fiscal years' Q4. No forecasting, comps,
valuation, or Excel work performed.

## 2. Sources used

All 24 manifest sources relevant to FY25–FY26 history: 10-Ks (SRC-001 not needed,
SRC-002, SRC-024), all six 10-Qs (SRC-003–005, SRC-006–008), all eight earnings
releases (SRC-009–016), and the FY26 Q4 slides (SRC-017). AI research reports
(SRC-019/020): not used for any value (verified programmatically, as in Gate 5A).

## 3. Population statistics (combined pilot + Gate 5B)

| Metric | Count |
|---|---|
| Total populated values (8 quarters + 2 annuals) | **839** |
| Reported | 475 |
| Calculated | 256 |
| Supplemental | 108 |
| Explicit not-disclosed determinations | 96 |
| Per-quarter range | 87 (FY25 Q2/Q3) – 95 (FY25 Q4, FY26 Q1, FY26 Q4) |
| Q4 derivation rows (both years combined) | 81 (37 FY25 + 44 FY26) |

## 4. Reconciliation checks

**107 checks total: 103 PASS · 0 FAIL · 4 BLOCKED** (70 new full-scope checks in
`orcl_historical_full_checks.csv`: 69 pass, 1 blocked; plus the 37 Gate 5A pilot
checks, still valid for their original FY26 Q1/Q4 scope: 34 pass, 3 blocked). No
failures anywhere. New this session: **CHECK_050 sum-of-quarters closed for both
fiscal years** — FY25 and FY26 quarterly revenue, operating income, net income,
depreciation, SBC, and cash flow all sum exactly (or within documented $1M
recast-rounding) to their respective 10-K annual figures (CHK25Q4-11/12/13,
CHKX-01/02/03/04/05/06/07). The single blocked check (CHK25Q4-09, FY25 quarterly
debt roll-forward) is a scope decision, not a data gap — deferred as optional Gate
6 follow-up.

## 5. New findings this session (D-016)

Two disclosure-architecture changes distinct from Q-18/D-013 were confirmed:
(a) **no dedicated lease footnote exists in the FY2025 Q1–Q3 10-Qs** — BS_060/
DEBT_050/DEBT_060 are genuinely not disclosed for those three quarters, first
appearing at FY2025 Q4/annual; (b) **FY2025 exact-millions IaaS/SaaS dollars**
(REV_120/REV_130) were never disclosed in their own period's release (headline
billions only) but were later published as recast comparatives in the FY2026 Q1
and Q4 releases — adopted as the primary value with the precision upgrade
documented in every row. Full detail: `10_Working_Data/raw_extractions/
GATE_5B_EXTRACTION_LOG.md`.

## 6. Conflicts — closure status

C-01 (gross debt) and C-02 (depreciation), resolved in Gate 5A at the annual level,
now have their **full quarterly series closed and tied**: gross debt across all
eight quarters (FY25 Q1 $84,515M → FY26 Q4 $129,541M, peaking at FY26 Q3
$134,605M before preferred-related paydown); depreciation FY25 804→908→1,003→1,152
and FY26 1,351→1,704→2,153→2,415, each set summing exactly to its 10-K annual
figure. C-06 (uncommenced leases) now has a trackable quarterly series (FY25 Q1
$36.2B → FY26 Q4 $260B) confirming the figure is a routinely-disclosed 10-Q/10-K
item, not a one-off. No new conflicts opened.

## 7. Architecture changes made

- **D-016**: documented the two disclosure-evolution findings above; amended
  dictionary notes for BS_060/DEBT_050/DEBT_060 and REV_120/REV_130; no field IDs
  changed, no prior Gate 5A values altered.
- **D-017**: established the full-extraction file pair
  (`orcl_historical_quarterly_full.csv` / `_full_provenance.csv`) as the Gate 6+
  input, built by importing the Gate 5A pilot's FY2026 Q1/Q4/annual entries
  verbatim (zero re-transcription, zero value drift) and adding the six new
  quarters. Pilot files retained unmodified as the audit trail.
- Template v2 (125 rows, from Gate 5A) used unchanged as the wide-file basis;
  original Gate 4 template still untouched.

## 8. Structural validation

Programmatic checks confirm: no duplicate field IDs (dictionary, mapping, full
file, template v2); dictionary and mapping remain 1:1 (137 fields); every
extracted-status provenance row cites an existing manifest source ID; every
`calculated` value carries a formula; every populated wide-file cell has a matching
provenance row and vice versa; the two dual-presentation caption families
(REV_010/020/COGS_010 vs. REV_011/021/147/COGS_011/OPEX_065) never co-populate the
wrong fiscal year; no source file in `01_`–`09_` was modified; the original
120-row template is byte-identical to its Gate 4 state; all CSVs parse. Zero
errors.

## 9. Is the extraction process safe to scale further?

Yes — this session was itself the scale-up test (2 quarters → 8 quarters + 2
annuals, ~3.4x the value count) and it held: zero failed checks, zero structural
errors, and the one new disclosure-evolution issue (D-016) was caught by the
process rather than silently mis-populated. The project is ready for Gate 6
(cross-source reconciliation beyond the intra-document/derivation checks already
run) whenever the user wants to proceed.

## 10. Remaining blockers (unchanged from Gate 5A, plus one new item)

D-014 EBITDA sign-off; transcripts (Q-04) and analyst-day deck (Q-05) still
missing; preferred-stock conversion terms need the Certificate of Designations/
prospectus (Q-11); user thesis template blank (Q-06); SRC-016 capture defect
(clipped wide tables, cosmetic only — did not block any value this session); new
optional item — FY25 quarterly debt roll-forward (CHK25Q4-09) if a trend view of
C-01 is wanted before Gate 9.

## 11. Exact next prompt (Gate 6)

> Continue the Oracle equity-research project. This session is Gate 6: historical
> reconciliation. Read CLAUDE.md, CURRENT_STATE.md, 00_project_control/ (especially
> this file and decision_log D-016/D-017), HISTORICAL_RECONCILIATION_PLAN.md, and
> the full extraction files in 10_Working_Data/raw_extractions/
> (orcl_historical_quarterly_full.csv + _full_provenance.csv) and
> 10_Working_Data/reconciliations/ (both checks files). Execute the Gate 6
> reconciliation battery exactly as specified in HISTORICAL_RECONCILIATION_PLAN.md
> §"Execution order at Gate 6": cross-document checks (release vs. filing) beyond
> what Gate 5A/5B already ran intra-document; any residual conflict entries;
> produce a consolidated Gate 6 checks dashboard. Do not begin forecasting,
> scenario design, comps, or the Excel model. Update project-control files, commit,
> and push on the designated branch.
