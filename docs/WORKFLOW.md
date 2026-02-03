# Workflow (Benchcraft Web)

This workflow is designed to keep **quality high** while increasing throughput:
small checkpoints, parallel lanes, and disciplined context management.

## Primary surface: Codex App

Use the Codex app as the control plane:

- One project = one sidebar entry.
- One checkpoint = one thread (keeps context clean).
- Prefer **worktree threads** for any non-trivial change.
- Use the **Review** pane for diffs, staging/reverting, and inline feedback.
- Use `/review` for an independent review agent.
- Use `/status` to monitor context usage and stop early if context is getting large.
- Use `/plan-mode` only when you need multi-step planning; execution is still checkpoint-based.

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

> This applies to “read-only” work too (reviews, design suggestions, doc audits).  
> Mark non-applicable gates as `N/A`, but still update `plans/NOW.md` and write a report.

## Parallel lanes (v1.1)

Use three lanes to move faster without losing control:

- **Lane A — Builder:** implement the next step (typically in a worktree).
- **Lane B — Reviewer:** independent review of diffs/PRs (`/review` and/or GitHub review).
- **Lane C — Tests/QA:** run quality gates and add/update tests when the plan requires it.

Keep lanes isolated by file ownership. Avoid multiple lanes changing dependencies or lockfiles.

## Worktrees for safe parallelism

Worktrees are the default mechanism for parallel work:

- Each lane runs in its own worktree with a clear scope.
- Integrate changes via **Sync with local** (or apply patch).
- Only commit when the human says so.

## Model + reasoning effort (recommended defaults)

Codex supports model variants and reasoning effort levels. Use these defaults unless you have a clear reason to deviate:

- Start with **Codex model + medium reasoning** for day-to-day coding and iterative UI work.
- Switch to **high** when tasks become multi-step, ambiguous, or require careful debugging/refactoring.
- Use **xhigh / “Extra High”** sparingly for the hardest tasks (deep debugging, large migrations, complex refactors).
- Use a **mini / lightweight Codex model** for simple edits (docs tweaks, small refactors, quick Q&A) to extend rate limits.

Record the chosen **model + reasoning effort** in each checkpoint report. This makes it easy to calibrate your presets over time.

## Dependency policy

- Dependency changes are approval-gated.
- Serialize dependency work: one active dependency-changing effort at a time.
- Always record dependency rationale in the checkpoint report.

## Branching and PRs

- Work on a feature branch.
- Push when a checkpoint is reviewable.
- Use the PR template (`.github/PULL_REQUEST_TEMPLATE.md`).
- Commit, merge, and rebases are user-controlled unless explicitly delegated.
- Merge only when quality gates pass and review is clean.

## Context hygiene

- Treat the repository as memory. Do not rely on chat history.
- Keep `plans/NOW.md` short. Link to ExecPlans and docs instead of pasting large context.
- Prefer one thread per checkpoint; archive threads when done.

## Doc improvement loop (optional, recommended)

After you polish a doc, run a **doc audit checkpoint**:

- Ask Codex to propose **3 targeted improvements** (no full rewrite).
- Capture suggestions in a checkpoint report.
- Convert accepted suggestions into small, checkpointable tasks in `plans/WORK_QUEUE.md`.

This keeps documents continuously improving without bloating context or causing churn.
