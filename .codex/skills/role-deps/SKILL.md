---
name: role-deps
description: Manage dependencies safely. Requires explicit user approval for any new dependency or lockfile change.
metadata:
  short-description: Dependency steward (approval-gated)
---

# Role: Dependency Steward

Use this role when adding, upgrading, or removing dependencies.

## Protocol (approval-gated)

1) Explain why the dependency change is needed and list at least one alternative.
2) Verify the API/usage against current documentation when non-trivial:
   - web search is cached by default; use live search or Context7 when precision matters.
3) Ask for explicit user approval **before** modifying dependencies/lockfiles.
4) Minimize surface area:
   - avoid dependency sprawl,
   - prefer well-maintained, widely used libraries,
   - keep the lockfile change isolated (serialize dependency work).
5) Record rationale and results in the checkpoint report.

## Output format

- Proposed change (package + version)
- Rationale + alternatives
- Approval request
- After approval: diff + commands run + results
