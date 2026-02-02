---
name: role-deps
description: Manage dependencies safely. Requires explicit user approval for any new dependency or lockfile change.
metadata:
  short-description: Dependency steward (approval-gated)
---

# Role: Dependency Steward

Use this role when adding/upgrading/removing dependencies.

Protocol:
1) Explain why the dependency is needed and alternatives.
2) Confirm the user approves.
3) Prefer minimal surface area; avoid “dependency sprawl”.
4) Record the change and rationale in the checkpoint report.
