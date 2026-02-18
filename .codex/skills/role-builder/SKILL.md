---
name: role-builder
description: Implement the next planned step safely: small diff, run checks, update plans/reports, then stop for review.
---

# Role: Builder

Use this role when **implementing** changes.

The workflow is:

**read → change → run gates → report → stop**

## Before you edit (mandatory)

1) Read `docs/exec-plans/active/NOW.md` and confirm:
   - one objective
   - one next step
   - timebox (15–30 min)

2) Read the sources of truth (as applicable):
   - Treat `docs/exec-plans/active/NOW.md` → **Read first** as the canonical list.
   - Do not maintain a separate read-first list here (prevents drift).

3) Plan hygiene:
   - Ensure `NOW.md → Active ExecPlan` points to a real plan folder, and the next step points to a real step sheet.
   - If plan/step sheet is missing or stale, switch to `.codex/skills/role-planner` first.

4) Scope/safety checks:
   - If the step requires dependency changes → **stop** and ask the human to apply them (see below).
   - If the step is review-only → do an audit-only checkpoint (no code changes) and write a report.

## Dependency changes (human-operated)

Dependency changes are approval-gated.

If you need a new package, a version bump, or any lockfile change:

1) Stop and write a short proposal:
   - what you want to change
   - why
   - at least one alternative
   - risks (maintenance/bundle/breaking changes)
2) Provide exact command(s) the human should run.
3) Wait for confirmation before continuing.

## Implementation rules

- Keep the diff small and reviewable.
- Avoid wrapper-only DOM nesting; prefer layout primitives and semantic HTML.
- Do not invent requirements. If something is unclear, update `docs/exec-plans/active/NOW.md` and stop.
- Do not commit unless explicitly instructed.

## Quality gates

Unless doc-only:

- Run `bun run lint` and `bun run typecheck`.
- Run tests when changes are user-facing, risky, or touch core flows. Otherwise mark tests as `N/A` with a reason.

If the repo does not expose scripts yet, mark gates as `N/A` and state why.

## End-of-checkpoint deliverables

1) Plan bookkeeping (keep it honest):
   - Mark the step done in the step sheet and in `EXECPLAN.md` (if completed).
   - If all steps are done, move the plan folder to `docs/exec-plans/completed/`.
   - Update `docs/exec-plans/active/NOW.md`:
     - mark the checkbox if done
     - set the next step (only one) or set Active ExecPlan to `N/A` if completed

2) Provide a reviewable diff (or file list + key snippets).

3) Write a checkpoint report in `reports/` using `reports/TEMPLATE.md`.

4) Stop for human review.
