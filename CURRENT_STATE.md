# CURRENT_STATE

Last updated: 2026-07-20 (branch-sync session — FY2026 10-K merged in and registered)
Branch: `claude/oracle-equity-model-mhmjq4` (tracks origin; remote = DrakeKrommenhoek/orcl-to-the-moon)

## Current phase

**Gate 4 COMPLETE.** Gates 1–3 completed earlier on 2026-07-20. **Gate 5 (data
extraction) is now ready to begin in the next session** — see readiness checklist below.
Gate 5 extraction was deliberately NOT started in this session (sync-only scope).

## Completed work

- Gates 1–3: inventory, manifest (23 sources), duplicate review, conflict register
  (C-01…C-11), governance file set.
- Gate 4: three-layer historical architecture, 132-field data dictionary, source-to-field
  mapping, disclosure matrix, blank extraction template, reconciliation plan, precedence
  rules, gate review. See prior CHANGELOG entries for the full file list.
- **Branch-sync session (this session):**
  - `origin/main` had received a direct upload (commit `d136102`, "Add files via upload")
    containing `ORCL_2026_10-K_FY_Ended_2026-05-31.pdf` at repo root.
  - Merged `origin/main` into this branch (merge commit, no conflicts; both branch
    histories preserved — no force-push, no rebase of shared history).
  - Verified filing identity: Form 10-K, Oracle Corporation, Commission File 001-35992,
    fiscal year ended May 31, 2026, signed 2026-06-22 by C. Magouyrk (CEO), M. Sicilia
    (co-CEO), H. Maxson (CFO); 139 pages; no MD5 duplicate against existing filings; not
    an LFS pointer (real ~2.0MB blob).
  - Moved it via `git mv` to `02_Annual_Filings/ORCL_2026_10-K_FY_Ended_2026-05-31.pdf`.
  - Registered it as **SRC-024** in `00_project_control/source_manifest.csv`.
  - Replaced all 64 occurrences of `SRC-024_RESERVED` with `SRC-024` in
    `10_Working_Data/architecture/source_to_field_mapping.csv`.
  - Annotated C-01, C-02, C-06 in `source_conflicts.md` and Q-01 in `open_questions.md`
    to reflect "source now available" — **explicitly did not resolve any of the three
    conflicts**, since resolving them requires reading the filing's actual disclosures,
    which is Gate 5/6 work.
  - Added a clarifying addendum to `00_project_control/GATE_4_REVIEW.md` (left the
    original gate-time text intact below it).

## Work in progress

None mid-flight. Clean stopping point.

## Known issues / blockers (Gate 5 scope, not yet done)

1. **SRC-024 content not yet extracted.** The filing exists and its identity is verified,
   but no numbers have been pulled from it. C-01 (gross debt), C-02 (depreciation), and
   C-06 (uncommenced lease commitments) remain **open** until Gate 5 extraction + Gate 6
   reconciliation.
2. All 8 earnings-call transcripts missing (Q-04); analyst-day deck missing (Q-05).
3. User thesis template still blank (Q-06) — blocks Gate 8.
4. EBITDA definition undecided (Q-10) — PROF_160 computation blocked.
5. FY26 filed-statement presentation change unverified (Q-18) — first thing to check at
   Gate 5, now directly checkable against SRC-024.
6. FactSet MCP connector present but unauthenticated (Q-08).
7. Research-report provider attribution (ChatGPT vs. Gemini) still unresolved (Q-02).

## Gate 5 readiness checklist

- [x] FY2026 10-K present (`02_Annual_Filings/ORCL_2026_10-K_FY_Ended_2026-05-31.pdf`)
- [x] Identity validated (Form 10-K, Oracle Corporation, FYE 2026-05-31)
- [x] Registered as SRC-024 in `source_manifest.csv`
- [x] Working branch includes latest relevant changes from `main` (merged, not rebased)
- [x] Working tree clean (confirmed pre-commit; re-confirm after this session's commit)
- [x] Updated branch pushed to `origin/claude/oracle-equity-model-mhmjq4`

**All conditions met as of this session's push. Gate 5 may begin next session.**

## Next recommended action

Full-scope Gate 5: extract FY2025 Q1 – FY2026 Q4 (including FY26 Q4/annual anchors and
the three previously-blocked conflicts) now that SRC-024 is in the repo.

## Exact restart prompt for the next session (Gate 5)

> Read CLAUDE.md, CURRENT_STATE.md, and all of 00_project_control/ (especially
> GATE_4_REVIEW.md — including its 2026-07-20 addendum, open_questions.md,
> decision_log.md, source_conflicts.md), then
> 11_Analysis/historical/HISTORICAL_DATA_ARCHITECTURE.md, HISTORICAL_RECONCILIATION_PLAN.md,
> and 10_Working_Data/architecture/EXTRACTION_PRECEDENCE_RULES.md. SRC-024 (the FY2026
> 10-K) is present in 02_Annual_Filings/ and already registered in source_manifest.csv —
> do not re-register it. Execute Gate 5 data extraction: populate a working copy of
> 10_Working_Data/templates/orcl_historical_quarterly_template.csv in
> 10_Working_Data/raw_extractions/ (the template itself stays blank) for FY2025 Q1 –
> FY2026 Q4 following the three-layer rules, the precedence ladder, and blank-beats-guess
> (D-011). Resolve Q-18 (FY26 statement captions) first by comparing SRC-024/SRC-006
> statement captions to SRC-003. Then use SRC-024 to work toward resolving C-01
> (gross debt), C-02 (depreciation), and C-06 (uncommenced lease commitments) — only
> after inspecting the actual filing disclosures directly, recording the resolution with
> section/page citations. Record source ID + section for every value; classify every cell
> reported/calculated; do not populate any Layer 3 stream except via the documented
> bridge; leave not-disclosed cells blank with status not_disclosed. Do not start Gate 6
> reconciliation beyond the intra-document checks needed to trust the transcription; do
> not build the Excel model.

## Restart note

If this file and the architecture docs disagree, the architecture docs govern structure;
this file governs sequencing/status.
