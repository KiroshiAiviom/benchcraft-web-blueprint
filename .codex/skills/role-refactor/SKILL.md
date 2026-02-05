---
name: role-refactor
description: Refactor code safely (preferably behavior-preserving). Requires an explicit plan and frequent safety checks.
metadata:
  short-description: Refactor (disciplined, checkpointed)
  recommended-model: codex
  recommended-reasoning: high
---

# Role: Refactor

Use this role for structural improvements: readability, maintainability, architecture hygiene, performance cleanup.

## Default model + effort

- Prefer **high** effort for refactors (they require consistency and careful reasoning).
- Use **xhigh** only for very large refactors/migrations when needed.

Record model/effort in the checkpoint report.

## Preconditions (must be true)

- There is an explicit refactor plan:
  - a dedicated refactor doc, or
  - an ExecPlan step that clearly describes refactor scope and stop conditions.

If the plan is missing or vague, update the plan before editing code.

## Core rules

- Prefer behavior-preserving refactors.
- If behavior must change, split it into a separate feature/bug plan (or a separate ExecPlan step).
- Keep diffs small and checkpointed (15–30 minutes).
- Do not mix refactors with feature work unless the plan explicitly allows it.
- Run quality gates frequently (lint/typecheck; tests when applicable).

## Refactor method (recommended)

1) Define invariants:
   - what must remain true (public APIs, UI behavior, performance constraints).
2) Identify the smallest safe slice:
   - one module, one boundary, one pattern at a time.
3) Make mechanical, reversible changes first:
   - rename, extract, move, simplify nesting.
4) Re-run gates and/or tests to validate invariants.
5) Stop with a clean diff and a report.

## Required outputs

At the end of each refactor checkpoint:

- `plans/NOW.md` updated (checkboxes reflect reality)
- checkpoint report in `reports/` including:
  - refactor intent
  - what changed and why
  - commands run + results
  - risks / follow-ups
  - model + effort used
- stop for human review
