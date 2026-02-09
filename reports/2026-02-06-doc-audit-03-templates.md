# Checkpoint Report — 2026-02-06 — Doc-audit 03 (Plans + templates)

## Objective

- Doc-audit (Plans + templates): propose exactly 3 improvements total across the audited files (no rewrites, no edits to audited files).

## Surface + model

- Surface: Codex app
- Worktree (if used): N/A
- Model + reasoning effort: GPT-5.3-Codex (medium)

## Summary

- Reviewed the Plans + templates bundle for instruction clarity, cross-doc consistency, and reviewer workflow fit.
- Identified 3 targeted improvements to reduce ambiguity and make audits/reviews more repeatable.

## Work performed

- Read `plans/NOW.md`, `plans/WORK_QUEUE.md`, `reports/TEMPLATE.md`, and the templates in `docs/templates/`.
- Checked for contradictions/ambiguity (especially around “what to output” and “what’s allowed to change”).
- Checked whether templates align with the `role-reviewer` output expectations (findings + recommendation).

## Findings (exactly 3 improvements)

### [P1] Make `plans/NOW.md` express checkpoint-specific audit constraints explicitly

- What’s wrong:
  - `plans/NOW.md` currently states “propose 3 improvements per bundle”, but individual audit checkpoints can have different constraints (for this checkpoint: exactly 3 improvements total; no edits to audited files except the checkbox; only a report file + checkbox update).
- Why it matters:
  - Creates avoidable ambiguity and increases the odds the agent produces the wrong output (wrong count, wrong scope, or edits to forbidden files).
- Proposed fix:
  - Add a small, dedicated “Constraints” subsection under the active `## Next step` item template (or a single “Constraints:” line) where each checkpoint can declare:
    - exact number of improvements expected,
    - allowed edit surface (e.g., “only `plans/NOW.md` checkboxes + new report”),
    - “no rewrites” / “no new docs” rules when applicable.

### [P2] Add a reviewer-friendly structure to `reports/TEMPLATE.md`

- What’s wrong:
  - `reports/TEMPLATE.md` does not include a standard place for “Findings (P0–P3)” nor an explicit “Approve / Request changes” recommendation, despite the `role-reviewer` output format expecting both.
- Why it matters:
  - Reviews/audits become inconsistent in structure, making it harder to scan and act on outcomes across checkpoints.
- Proposed fix:
  - Add two short sections to `reports/TEMPLATE.md`:
    - `## Findings (P0–P3)` (with guidance: what’s wrong → why → fix),
    - `## Recommendation (approve/request changes)` (1 line).

### [P2] Make `docs/templates/EXECPLAN_TEMPLATE.md` reference fallbacks when canonical docs don’t exist yet

- What’s wrong:
  - `docs/templates/EXECPLAN_TEMPLATE.md` references only `docs/PRD.md`, `docs/TECH_SPEC.md`, `docs/DESIGN_SYSTEM.md`, but those files may not exist early in a repo (and this repo currently relies on templates).
- Why it matters:
  - Encourages broken links and forces the agent to guess where the source-of-truth lives, increasing drift between plan and docs.
- Proposed fix:
  - Mirror the fallback language used in `plans/NOW.md`, e.g.:
    - `docs/PRD.md` (or `docs/templates/PRD_TEMPLATE.md`)
    - `docs/TECH_SPEC.md` (or `docs/templates/TECH_SPEC_TEMPLATE.md`)
    - `docs/DESIGN_SYSTEM.md` (or `docs/templates/DESIGN_SYSTEM_TEMPLATE.md`)

## Files changed

- `reports/2026-02-06-doc-audit-03-templates.md`

## Commands run + results

- N/A (doc-only audit; used read-only commands like `ls` and `sed` to inspect files)

## Definition of Done check

- Minimum checkpoint DoD: pass (report written; `plans/NOW.md` updated; stopped for review)
- UI DoD (if applicable): N/A (doc-only)
- Dependency DoD (if applicable): N/A (no dependency changes)
- Quality gates: N/A (doc-only; no lint/typecheck/test change surface)

## Risks / open issues

- Current templates can unintentionally drive inconsistent outputs (missing “findings + recommendation” structure) and ambiguity when canonical docs do not exist yet (ExecPlan references).

## Next step suggestion

- N/A (per checkpoint rule: stop after report + `plans/NOW.md` checkbox update)
