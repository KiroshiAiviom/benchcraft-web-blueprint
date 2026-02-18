---
name: role-refactor
description: Refactor code safely (preferably behavior-preserving). Requires an explicit plan and frequent safety checks.
---

# Role: Refactor

Use this role for structural improvements: readability, maintainability, architecture hygiene, performance cleanup.

## Preconditions (must be true)

- There is an explicit refactor plan:
  - an ExecPlan step that clearly describes refactor scope and stop conditions, or
  - a dedicated refactor doc.

If the plan is missing or vague, update the plan before editing code.

## Core rules

- Prefer behavior-preserving refactors.
- If behavior must change, split it into a separate feature/bug plan (or a separate ExecPlan step).
- Keep diffs small and checkpointed (15–30 minutes).
- Do not mix refactors with feature work unless the plan explicitly allows it.
- Run quality gates frequently (lint/typecheck; tests when applicable).

## Pre-flight (before the first edit)

1) Capture **3–5 invariants** that must remain true (APIs, UX behavior, performance constraints).
2) Run the smallest available baseline gate (or mark `N/A` with a reason):
   - `bun run lint`
   - `bun run typecheck`
   - relevant tests when the risk warrants it

Record invariants + baseline status in the checkpoint report so regressions are easier to diagnose.

## Refactor method (recommended)

1) Define invariants (what must remain true).
2) Identify the smallest safe slice (one module/boundary/pattern at a time).
3) Make mechanical, reversible changes first (rename, extract, move, simplify nesting).
4) Re-run gates and/or tests to validate invariants.
5) Stop with a clean diff and a report.

## Required outputs

At the end of each refactor checkpoint:

- Plan bookkeeping updated (step sheet + `EXECPLAN.md` checkboxes + `NOW.md`)
- checkpoint report in `reports/` including:
  - refactor intent
  - what changed and why
  - commands run + results
  - risks / follow-ups
- stop for human review

Reference: `docs/QUALITY_SCORE.md`.
