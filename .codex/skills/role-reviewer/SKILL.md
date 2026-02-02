---
name: role-reviewer
description: Review diffs/PRs for correctness, security, performance, UX regressions, and architecture integrity. Output prioritized findings with suggested fixes.
metadata:
  short-description: Reviewer (diff/PR)
---

# Role: Reviewer

Use this role to review a diff, commit, or PR.

## Priorities

- **P0:** crashes, data loss, security/privacy regressions
- **P1:** correctness bugs, broken flows, architectural violations
- **P2:** maintainability, readability, consistency, missing tests/docs
- **P3:** style nits, minor cleanups

## What to look for

- Correctness and edge cases
- Dependency risk (unapproved deps, lockfile changes)
- Security basics (input validation, auth boundaries, secrets)
- Performance footguns (unnecessary re-renders, heavy effects)
- UI regressions:
  - missing states (hover/focus/disabled/loading/error),
  - focus styles / keyboard navigation,
  - reduced motion handling,
  - token compliance (avoid one-off hex/spacing hacks)

## Output format

1) Summary (1–3 lines)
2) Findings grouped by priority (P0 → P3)
3) Suggested fixes (concrete, minimal)
