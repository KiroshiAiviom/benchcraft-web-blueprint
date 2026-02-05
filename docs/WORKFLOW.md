# Workflow (Benchcraft Web)

This workflow keeps **quality high** while increasing throughput via:

- small, checkpointed diffs
- parallel work lanes with worktrees
- disciplined context management

## Primary surface: Codex App

Use the Codex app as the control plane:

- One project = one sidebar entry.
- One checkpoint = one thread (keeps context clean).
- Prefer worktrees for any non-trivial change or parallelism.
- Use the built-in diff/review UI to stage/revert and give precise feedback.

If you use the Codex CLI/IDE extension, the same principles apply: **one checkpoint per session** and **small diffs**.

## Documentation-first (keep it lean)

Before serious coding begins, create/fill the three canonical docs:

- `docs/PRD.md` — scope, routes/flows, features + acceptance criteria
- `docs/DESIGN_SYSTEM.md` — typography, palette, tokens, layout primitives, component rules
- `docs/TECH_SPEC.md` — pinned stack, architecture, backend/data contracts, deployment notes

Templates live in `docs/templates/`.

If any of these are missing and the task is non-trivial, the agent should propose creating them **before** implementing.

## Core loop (one checkpoint)

Every iteration is:

**1 task → 1 checkpoint → report → stop**

1) Read `plans/NOW.md` and execute **only the single next step**.
2) Timebox to **15–30 minutes**.
3) End the checkpoint with:
   - a reviewable diff,
   - an updated `plans/NOW.md` (checkboxes reflect reality),
   - a checkpoint report in `reports/` (use `reports/TEMPLATE.md`),
   - quality gates (lint/typecheck; tests when appropriate; otherwise `N/A` with a reason),
   - then **stop** for human review.

> This applies to read-only work too (reviews, design suggestions, doc audits).

## Parallel lanes

Use three lanes to move faster without losing control:

- **Lane A — Builder:** implement the next step (typically in a worktree).
- **Lane B — Reviewer:** independent review of diffs/PRs.
- **Lane C — Tests/QA:** run quality gates and add/update tests when the plan requires it.

Keep lanes isolated by file ownership. Avoid multiple lanes changing dependencies or lockfiles.

## Worktrees for safe parallelism

Worktrees are the default mechanism for parallel work:

- Each lane runs in its own worktree with a clear scope.
- Integrate changes via the app’s sync/apply workflow, or by cherry-picking.
- Only commit when the human says so.

## Dependency policy

- Dependency changes are approval-gated.
- Serialize dependency work: one active dependency-changing effort at a time.
- Always record dependency rationale in the checkpoint report.

## Context hygiene

- Treat the repository as memory. Do not rely on chat history.
- Keep `plans/NOW.md` short. Link to docs/ExecPlans instead of pasting large context.
- Prefer one thread per checkpoint; archive threads when done.

## Doc improvement loop (optional, recommended)

After you polish a doc, run a **doc audit checkpoint**:

- Ask Codex to propose **3 targeted improvements** (no full rewrite).
- Capture suggestions in a checkpoint report.
- Convert accepted suggestions into small tasks in `plans/WORK_QUEUE.md`.

This keeps documents improving without bloating context or causing churn.
