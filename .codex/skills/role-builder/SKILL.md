---
name: role-builder
description: Implement the next planned step safely: small diff, run checks, update plans/reports, then stop for review.
metadata:
  short-description: Builder (checkpoint-based implementation)
  recommended-surface: codex app (worktree)
  recommended-model: gpt-5.2-codex
  recommended-reasoning: medium
---

# Role: Builder

Use this role when **implementing** code changes.

## Default model + effort

- Default: a Codex-optimized model at **medium** reasoning effort.
- Escalate to **high** when debugging is non-trivial or changes span multiple files/modules.
- Use **xhigh** sparingly for the hardest problems (deep debugging, large refactors/migrations).

Always record the chosen model/effort in the checkpoint report.

## Before you edit anything (mandatory checklist)

1) Read `plans/NOW.md` and confirm:
   - one objective,
   - one next step,
   - timebox (15–30 minutes).

2) Read quality rules:
   - `docs/DOD.md`
   - `docs/UI_FOUNDATION_PACK.md`
   - `docs/STYLE_GUIDE.md` / `docs/UI_SPEC.md` if they exist.

3) Confirm scope and safety:
   - If the step requires changing dependencies → **stop** and switch to `role-deps`.
   - If the step is “review only” → use `role-reviewer` instead.

4) Decide which gates you can run this checkpoint:
   - lint + typecheck (default)
   - tests when risk warrants it or when the plan requires it

If the repo does not have scripts yet, plan to mark gates as `N/A` with a reason.

## Implementation rules

- Keep the diff small and reviewable.
- Prefer worktrees for any non-trivial change.
- Avoid wrapper-only DOM nesting; use layout primitives and semantic HTML.
- Use tokens for UI (no one-off hex colors/spacing hacks).
- Add interaction states where applicable (hover/focus/active/disabled/loading/error).
- Do not “invent requirements”. If something is unclear, update the plan and stop.

## Dependency and commit discipline

- **Dependencies:** never add/upgrade/remove without explicit user approval.
- **Commits:** do not commit unless explicitly instructed. Prepare a clean diff and stop.

## End-of-checkpoint deliverables (required)

1) Update `plans/NOW.md`:
   - mark the step checkbox if done,
   - adjust the next step if reality changed (keep it one step).

2) Produce a reviewable diff:
   - show the diff, or list files + key snippets.

3) Run gates when available:
   - `lint`
   - `typecheck`
   - tests if applicable  
   If unavailable, write `N/A` with a reason.

4) Write a checkpoint report in `reports/` (use `reports/TEMPLATE.md`):
   - objective, summary, files changed
   - commands + results
   - DoD check (pass/fail/N/A)
   - risks/open issues
   - next step suggestion
   - surface + model + reasoning effort

5) Stop for human review.

## Anti-patterns (do not do these)

- Large “kitchen sink” diffs that combine multiple concerns.
- Silent dependency changes (including lockfile churn).
- Skipping gates when scripts exist.
- Refactoring while implementing a feature unless the plan explicitly says so.
