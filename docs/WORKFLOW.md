# Workflow (Benchcraft Web)

This document defines how we work with Codex to keep quality high while moving fast:
small checkpoints, parallel review/testing, and clean context management.

## Core loop (one checkpoint)

Every iteration is:

**1 task → 1 checkpoint → report → stop**

1) Read `plans/NOW.md` and execute **only the single next step**.
2) Timebox the checkpoint to **15–30 minutes**.
3) End the checkpoint with:
   - a reviewable diff,
   - a short checkpoint report (`reports/`),
   - plan updates that reflect reality,
   - quality gates (lint/typecheck; tests when appropriate),
   - then **stop** for human review.

## Parallel lanes (v1.0)

We run three lanes to increase throughput without losing control:

- **Lane A — Local Builder:** implementation in small checkpoints.
- **Lane B — Reviewer:** independent review of diffs/PRs (local `/review` and/or GitHub review).
- **Lane C — Tests/QA:** add/update tests and run them independently.

Keep lanes isolated by file ownership. Avoid multiple lanes changing dependencies or lockfiles.

## Branching and PRs

- Work on a feature branch.
- Push when the checkpoint is reviewable.
- Use the PR template (`.github/PULL_REQUEST_TEMPLATE.md`).
- Merge only when quality gates pass and review is clean.

## Dependency policy

- Dependency changes are approval-gated.
- Serialize dependency changes: one active dependency-changing effort at a time.
- Always record dependency rationale in the checkpoint report.

## Context hygiene

- Treat the repository as memory. Do not rely on chat history.
- Keep `plans/NOW.md` short. Link to ExecPlans and docs instead of pasting large context.
- Prefer one Codex session per checkpoint.

