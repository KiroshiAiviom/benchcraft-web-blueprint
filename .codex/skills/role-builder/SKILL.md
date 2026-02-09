---
name: role-builder
description: Implement the next planned step safely: small diff, run checks, update plans/reports, then stop for review.
metadata:
  short-description: Builder (checkpoint-based implementation)
  recommended-surface: codex app (worktree)
  recommended-model: GPT-5.3-Codex
  recommended-reasoning: medium
---

# Role: Builder

Use this role when **implementing** changes.

The workflow is:

**read → change → run gates → report → stop**

## Before you edit (mandatory)

1) Read `plans/NOW.md` and confirm:
   - one objective
   - one next step
   - timebox (15–30 min)

2) Read the sources of truth (as applicable):
   - Treat `plans/NOW.md` → **Read first** as the canonical list.
   - Do not maintain a separate read-first list here (prevents drift).

3) Scope/safety checks:
   - If the step requires dependency changes → **stop** and switch to `role-deps`.
   - If the step is review-only → use `role-reviewer`.

## Implementation rules

- Keep the diff small and reviewable.
- Avoid wrapper-only DOM nesting; prefer layout primitives and semantic HTML.
- Do not invent requirements. If something is unclear, update `plans/NOW.md` and stop.
- Do not commit unless explicitly instructed.

## Quality gates

Unless doc-only:

- Run `bun run lint` and `bun run typecheck`.
- Run tests when changes are user-facing, risky, or touch core flows. Otherwise mark tests as `N/A` with a reason.

If the repo does not expose scripts yet, mark gates as `N/A` and state why.

## End-of-checkpoint deliverables

1) Update `plans/NOW.md`:
   - mark the step checkbox if done
   - set the next step (only one)

2) Provide a reviewable diff (or file list + key snippets).

3) Write a checkpoint report in `reports/` using `reports/TEMPLATE.md`.

4) Stop for human review.
