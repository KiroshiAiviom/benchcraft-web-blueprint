# Workflow (Benchcraft Web)

This workflow keeps **quality high** while increasing throughput via:

- small, checkpointed diffs
- parallel work lanes with worktrees
- disciplined context management
- agent-managed planning artifacts (ExecPlans)

## Primary surface: Codex App

Use the Codex app as the control plane:

- One project = one sidebar entry.
- One checkpoint = one thread (keeps context clean).
- Prefer worktrees for any non-trivial change or parallelism.
- Use the built-in diff/review UI to stage/revert and give precise feedback.

If you use the Codex CLI/IDE extension, the same principles apply: **one checkpoint per thread** and **small diffs**.

## Model + reasoning effort

- Default model: **GPT-5.3-Codex** (Codex App label; config id: `gpt-5.3-codex`).
- Default reasoning effort: **medium**. Use **high** when stuck / complex. Use **xhigh** (“extra high”) only for the hardest tasks.
- This blueprint pins model + default effort in `.codex/config.toml`.

## Documentation-first (keep it lean)

Before serious coding begins, create/fill the minimal set of project “source of truth” docs.

Planning note: drafting these docs in a separate planning session (often easier in ChatGPT) is usually faster than doing it mid-implementation.

**Recommended minimum:**

1) Product specs (what + acceptance criteria)
   - `docs/product-specs/index.md`
   - `docs/product-specs/<feature>.md` (copy `docs/product-specs/_TEMPLATE.md`)

2) Design System (tokens + primitives)
   - `docs/DESIGN_SYSTEM.md` (from `docs/templates/DESIGN_SYSTEM_TEMPLATE.md`)

3) Technical Spec (pinned decisions)
   - `docs/TECH_SPEC.md` (from `docs/templates/TECH_SPEC_TEMPLATE.md`)

Optional (but useful for enterprise work):

- Design decision records: `docs/design-docs/` (start with `core-beliefs.md`)
- Architecture map: `ARCHITECTURE.md` (keep it short; link out)

If key docs are missing and the task is non-trivial, the agent should propose creating them **before** implementing.

## Core loop (one checkpoint)

Every iteration is:

**1 task → 1 checkpoint → report → stop**

1) Drive the checkpoint from `docs/exec-plans/active/NOW.md` and execute **only the single next step**.
2) Timebox to **15–30 minutes**.
3) End the checkpoint with:
   - a reviewable diff,
   - updated plan bookkeeping (step sheet + checkboxes + next step),
   - a checkpoint report in `reports/` (use `reports/TEMPLATE.md`),
   - quality gates (lint/typecheck; tests when appropriate; otherwise `N/A` with a reason),
   - then **stop** for human review.

> This applies to read-only work too (reviews, design suggestions, doc audits).

## ExecPlans (agent-managed by default)

ExecPlans are stored under `docs/exec-plans/active/` and archived to `completed/`.

To reduce repetitive work, the agent may:

- create an ExecPlan when missing
- pick the next step (first unchecked)
- create/update a short step sheet for the checkpoint
- archive finished plans

Skill: `.codex/skills/role-planner`.

## Parallel lanes

Use lanes to move faster without losing control:

- **Lane A — Builder:** implement the next step (typically in a worktree).
- **Lane B — Review:** review diffs/PRs (human + built-in review UI).
- **Lane C — Tests/QA:** run quality gates and add/update tests when the plan requires it.

Keep lanes isolated by file ownership. Avoid multiple lanes changing dependencies or lockfiles.

## Worktrees for safe parallelism

Worktrees are the default mechanism for parallel work:

- Each lane runs in its own worktree with a clear scope.
- Integrate changes via the app’s sync/apply workflow, or by cherry-picking.
- Only commit when the human says so.

## Dependency policy

- Dependency changes are approval-gated.
- When a new dependency is required, the agent should propose it and ask the human to apply it.
- Serialize dependency work: one active dependency-changing effort at a time.
- Always record dependency rationale in the checkpoint report.

## Context hygiene

- Treat the repository as memory. Do not rely on chat history.
- Keep `docs/exec-plans/active/NOW.md` short. Link to long docs; don’t paste them.
- Prefer one thread per checkpoint; archive threads when done.

## Doc improvement loop (optional, recommended)

After you polish a doc, run a **doc audit checkpoint**:

- Ask Codex to propose **3 targeted improvements** (no full rewrite).
- Capture suggestions in a checkpoint report.
- Convert accepted suggestions into small tasks in your issue tracker (or `docs/exec-plans/active/NOW.md → Parking lot`).

This keeps documents improving without bloating context or causing churn.
