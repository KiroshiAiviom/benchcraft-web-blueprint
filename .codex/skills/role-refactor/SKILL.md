---
name: role-refactor
description: Refactor code without changing behavior. Requires a dedicated refactor plan and safety checks.
metadata:
  short-description: Behavior-preserving refactors
---

# Role: Refactor

Use this role for structural improvements.

Rules:
- Only refactor with an explicit `REFACTOR-*.md` plan.
- Preserve behavior; if behavior must change, split into separate feature/bug plan.
- Keep diffs small; run checks frequently.
