# Doc Audit 04 — Skills Bundle

- Date: 2026-02-06
- Surface: Codex desktop app
- Model: GPT-5.3-Codex
- Reasoning effort: medium
- Scope: Documentation-only audit of skill files (no skill file edits in this checkpoint)

## Files Reviewed

- `.codex/skills/ui-foundation-pack/SKILL.md`
- `.codex/skills/role-builder/SKILL.md`
- `.codex/skills/role-reviewer/SKILL.md`
- `.codex/skills/role-tests/SKILL.md`
- `.codex/skills/role-deps/SKILL.md`
- `.codex/skills/role-refactor/SKILL.md`

## Findings (Exactly 3 Improvements Proposed)

### 1) Reduce “Read-first” drift by making `plans/NOW.md` the single canonical checklist

Problem:
Multiple skills restate “read-first” lists with slight differences. Over time this tends to drift and makes it unclear which list is authoritative.

Proposed improvement:
In each skill that currently enumerates sources-of-truth, add a short note that `plans/NOW.md` “Read first” is the canonical list, and keep the skill’s list to *only* deltas (e.g., “if UI: also read `docs/UI_FOUNDATION_PACK.md`”). This is a small documentation tweak that prevents future inconsistency without changing workflow.

Applies to:
`ui-foundation-pack`, `role-builder` (and optionally `role-tests` / `role-reviewer` for consistency).

### 2) Align reviewer outputs with DoD by requiring “commands/gates status” in `role-reviewer`

Problem:
`role-reviewer` defines findings and priorities clearly, but it doesn’t explicitly require the “commands run” / “quality gates status” line items that `docs/DOD.md` expects even for read-only checkpoints (as `N/A` + reason). This makes reports inconsistent depending on who is running the review.

Proposed improvement:
Add a short “Required outputs” section to `role-reviewer` mirroring the DoD report minimums:
include “Commands run (or N/A + reason)” and “Quality gates (pass/fail/N/A + reason)”, plus confirm `plans/NOW.md` updated. Keep it brief and compatible with docs-only reviews.

Applies to:
`role-reviewer` (primary). Consider a one-line pointer in `role-builder` (“If review-only, ensure reviewer output includes gates status per DoD.”).

### 3) Make stop-conditions explicit for refactors by requiring a pre-change “invariants + quick baseline” note

Problem:
`role-refactor` correctly requires an explicit plan and emphasizes invariants, but it does not explicitly require capturing them *before* edits begin, nor does it nudge a minimal baseline (e.g., current lint/typecheck/test state) when available. In practice this leads to harder-to-diagnose regressions mid-refactor.

Proposed improvement:
Add a lightweight pre-flight step to `role-refactor`:
record 3–5 invariants + run the smallest available baseline gate (or mark `N/A` with reason) before the first edit. This makes “behavior-preserving” refactors more defensible with minimal overhead.

Applies to:
`role-refactor` (primary). Optionally cross-reference from `role-tests` (“baseline gates before/after when refactor risk is non-trivial”).

## Quality Gates

- `bun run lint`: N/A (doc-only checkpoint; no code/skill changes)
- `bun run typecheck`: N/A (doc-only checkpoint; no code/skill changes)
- Tests: N/A (doc-only checkpoint; no code/skill changes)

## Commands Run

- N/A (read-only inspection via file view; no repo scripts executed)

