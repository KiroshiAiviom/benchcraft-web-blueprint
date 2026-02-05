# Benchcraft Web — Agent Instructions

These are the operating rules for Codex when working in a repository using the Benchcraft Web workflow.

## Read-first order

1) `plans/NOW.md` — the current objective and the only next step.
2) The files listed under **“Read first”** inside `plans/NOW.md`.
3) `docs/DOD.md` — quality bar for completion.
4) `plans/WORK_QUEUE.md` — progress bridge and what’s next.

When the current work touches UI, also read:

- `docs/UI_FOUNDATION_PACK.md`
- `docs/DESIGN_SYSTEM.md` (if present)

## Core rules

- **One checkpoint per thread.** Do one step, produce a diff and a short report, then stop.
- **Small diffs.** Prefer multiple small checkpoints over a single large change.
- **No undocumented decisions.** If something is unclear or missing, update `plans/NOW.md` or the relevant canonical doc, then stop.
- **No surprise deps.** Any new dependency requires explicit approval (use the Deps skill).

## Quality gates

Unless the checkpoint is doc-only:

- Run `bun run lint` and `bun run typecheck`.
- Run tests when the change is user-facing, risky, or touches core flows. Otherwise mark tests as `N/A` with a reason.

## How instructions layer

- `AGENTS.md` applies globally.
- `AGENTS.md` in a subfolder **adds** constraints for that subtree.
- `AGENTS.override.md` (if used) is an emergency, temporary override for that folder/worktree.
