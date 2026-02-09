# Checkpoint Report — 2026-02-06 — DOC-AUDIT 01 (Core bundle)

## Objective

- Doc-audit (Core bundle): propose exactly 3 targeted improvements (no rewrites; no doc edits in this checkpoint).

## Surface + model

- Surface: Codex app
- Worktree (if used): N/A
- Model + reasoning effort: GPT-5.3-Codex, medium

## /status output

```text
## main...origin/main
```

## Files reviewed

- `AGENTS.md`
- `docs/WORKFLOW.md`
- `docs/SETUP.md`
- `docs/DOD.md`
- `docs/STACK_BASELINE.md`

## Improvements (exactly 3)

### 1) docs/WORKFLOW.md — Clarify “checkpoint” scope (thread vs session)

- What to change:
  - Replace “one checkpoint per session” wording with “one checkpoint per thread” to match `AGENTS.md` and reduce ambiguity.
- Why:
  - “Session” can mean a long-lived Codex project sidebar entry; the workflow elsewhere consistently uses “thread” as the unit of a checkpoint.
- Minimal suggested edit snippet:
  ```md
  If you use the Codex CLI/IDE extension, the same principles apply: **one checkpoint per thread** and **small diffs**.
  ```
- Impact:
  - Fewer interpretation errors (especially when a human runs multiple checkpoints in one “session” but separate threads).
- Risk:
  - Low; terminology-only clarification.

### 2) docs/SETUP.md — Make blueprint “overlay” instruction safer (avoid clobbering)

- What to change:
  - Add an explicit “merge, don’t overwrite” note before the “Copy the blueprint files/folders…” list.
- Why:
  - New users may blindly copy folders and overwrite existing repo state (especially `.github/`, `docs/`, `plans/`), causing accidental loss/churn.
- Minimal suggested edit snippet:
  ```md
  Copy/merge the blueprint files/folders into your new repo root (avoid overwriting existing files; prefer selective merges):
  
  - `AGENTS.md`
  - `.codex/`
  - `docs/`
  ```
- Impact:
  - Reduces accidental destructive “setup” outcomes; aligns with “small diffs / no surprise changes.”
- Risk:
  - Low; adds one caution line.

### 3) docs/STACK_BASELINE.md — Consolidate quality-gates guidance into docs/DOD.md

- What to change:
  - Replace the current “Quality gates” bullets with a single pointer to `docs/DOD.md` as canonical.
- Why:
  - The same guidance exists (in more detail) in `docs/DOD.md`; duplication risks drift (one doc updated, the other not).
- Minimal suggested edit snippet:
  ```md
  ## Quality gates (default expectations)
  
  See `docs/DOD.md` for checkpoint-level quality gates and when to run tests.
  ```
- Impact:
  - Less duplication and lower maintenance burden; clearer “source of truth.”
- Risk:
  - Low; readers lose the inline bullets but gain a canonical pointer.

## Summary

- Reviewed core workflow docs and identified 3 low-risk, consolidation-oriented edits.
- No documentation files were edited in this checkpoint (report + plan update only).

## Files changed

- `reports/2026-02-06-doc-audit-01-core.md`
- `plans/NOW.md`

## Commands run + results

- `git status -sb` (clean)
- Quality gates: N/A (doc-only checkpoint)

## Definition of Done check

- Minimum checkpoint DoD: pass (report written; plan checkbox updated; quality gates N/A for doc-only)
- UI DoD (if applicable): N/A (no UI changes)
- Dependency DoD (if applicable): N/A (no dependency changes)

