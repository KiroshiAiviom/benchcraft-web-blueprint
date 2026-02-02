---
name: role-refactor
description: Refactor code without changing behavior. Requires a dedicated refactor plan and safety checks.
metadata:
  short-description: Behavior-preserving refactors
---

# Role: Refactor

Use this role for structural improvements (readability, maintainability, architecture hygiene).

## Rules

- Only refactor with an explicit plan (`REFACTOR-*.md`).
- Preserve behavior. If behavior must change, split it into a separate feature/bug plan.
- Keep diffs small and checkpointed.
- Avoid mixing refactors with feature work.
- Run quality gates frequently (lint/typecheck; tests when applicable).

## Output format

- Refactor intent (what problem is being solved)
- Summary of changes
- Commands run + results
- Any follow-ups required
