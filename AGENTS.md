# Benchcraft Web — Agent Guide

This file is intentionally short.
Treat it as a **map**, not the encyclopedia.

## Start here (every thread)

1) Read `docs/exec-plans/active/NOW.md`.
2) Read **only** the files listed in `NOW.md → Read first` (keep that list small).
3) Execute exactly the **single** checkbox under `NOW.md → Next step` (timebox: 15–30 min).

(Plan index: `docs/PLANS.md`.)

## Bootstrap mode (fresh template repos)

Use this mode only when starting a new project and the canonical project docs don’t exist yet.

Rules:

- If `docs/TECH_SPEC.md` or `docs/DESIGN_SYSTEM.md` is missing, start from their templates.
- The first checkpoint should create minimal project docs:
  - at least one **Product Spec**: `docs/product-specs/<spec>.md`
  - `docs/TECH_SPEC.md`
  - `docs/DESIGN_SYSTEM.md`
- After those exist, run the normal checkpoint loop.

## Non-negotiables

- **One checkpoint per thread.** Small diff, then stop for human review.
- **Don’t invent requirements.** If something is unclear, write the question + assumption(s) into `docs/exec-plans/active/NOW.md`, then stop.
- **Report honestly.** Include commands run + results (or `N/A` + a reason).
- **No surprise dependencies.** Do not edit `package.json` or lockfiles unless the human explicitly approves.

## Dependencies (human-operated)

If you need a new package, version bump, or lockfile change:

1) Stop and write a short proposal:
   - what you want to change
   - why
   - at least one alternative
   - risks (maintenance/bundle/breaking changes)
2) Provide the exact command(s) the human should run.
3) Wait for confirmation before continuing.

## Skills / roles

Pick the smallest role that matches the work:

- `.codex/skills/role-planner` — create/maintain ExecPlans + step sheets; keep `NOW.md` in sync; archive completed plans
- `.codex/skills/role-builder` — implement the next planned step
- `.codex/skills/role-tests` — run quality gates / triage failures
- `.codex/skills/role-refactor` — refactors (invariants + baseline first)
- `.codex/skills/role-ui` — UI/UX work (audit/build protocol)

## Quality bar

- Source of truth: `docs/QUALITY_SCORE.md`.

## How instructions layer

- Root `AGENTS.md` applies repo-wide.
- `AGENTS.md` in a subfolder **adds** constraints for that subtree.
- `AGENTS.override.md` is an emergency, temporary override for that folder/worktree.
