# Workflow (Benchcraft Web)

This document defines how we work with Codex to keep quality high while moving fast:
small checkpoints, parallel review/testing, and clean context management.

## Primary surface: Codex App

Use the **Codex app** as the control plane:

- One project = one sidebar entry.
- One checkpoint = one thread (keeps context clean).
- Prefer **Worktree** threads for any non-trivial change.
- Use the **Review** pane for diffs, staging/reverting, and inline feedback.
- Use `/review` for an independent code review agent (review comments show up inline).
- Use `/status` to monitor context usage; stop early if context is getting large.
- Use `/plan-mode` only when you need multi-step planning; still execute in checkpoints.

## Core loop (one checkpoint)

Every iteration is:

**1 task → 1 checkpoint → report → stop**

1) Read `plans/NOW.md` and execute **only the single next step**.
2) Timebox the checkpoint to **15–30 minutes**.
3) End the checkpoint with:
   - a reviewable diff,
   - a short checkpoint report (`reports/`),
   - plan updates that reflect reality,
   - quality gates (lint/typecheck; tests when appropriate; or `N/A` with a reason),
   - then **stop** for human review.

## Parallel lanes (v1.1)

We run three lanes to increase throughput without losing control:

- **Lane A — Builder:** implement the next step (typically in a Worktree).
- **Lane B — Reviewer:** independent review of diffs/PRs (`/review` and/or GitHub review).
- **Lane C — Tests/QA:** run quality gates and add/update tests as needed.

Keep lanes isolated by file ownership. Avoid multiple lanes changing dependencies or lockfiles.

## Worktrees for parallelism

Worktrees are the default mechanism for safe parallel work.

- Each lane runs in its own worktree with a clear scope.
- Integrate changes back into your main checkout/feature branch via **Sync with local**.
- Prefer the “apply” approach (patch) when you want to keep your local commit history intact.
- Only commit when you (the human) say so.

## Branching and PRs

- Work on a feature branch.
- Push when the checkpoint is reviewable.
- Use the PR template (`.github/PULL_REQUEST_TEMPLATE.md`).
- Commit, merge, and rebases are user-controlled unless explicitly delegated.
- Merge only when quality gates pass and review is clean.

## Dependency policy

- Dependency changes are approval-gated.
- Serialize dependency changes: one active dependency-changing effort at a time.
- Always record dependency rationale in the checkpoint report.

## Context hygiene

- Treat the repository as memory. Do not rely on chat history.
- Keep `plans/NOW.md` short. Link to ExecPlans and docs instead of pasting large context.
- Prefer one thread per checkpoint; archive threads when done.
