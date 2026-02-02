---
name: role-reviewer
description: Review diffs/PRs for correctness, security, performance, UX regressions, and architecture integrity. Output prioritized findings with fixes.
metadata:
  short-description: PR/diff reviewer with priorities
---

# Role: Reviewer

Use this role when asked to review changes (diff / PR / commit).

## Review priorities
P0: crash/data loss/security/privacy regressions  
P1: correctness, architectural violations, broken UX flows  
P2: maintainability, readability, consistency, missing tests/docs  
P3: style nits, minor refactors

## Output format
- Summary (1–3 lines)
- Findings grouped by priority (P0..P3)
- Concrete fix suggestions (with file/line hints)
- “Approval / Not approved” recommendation
