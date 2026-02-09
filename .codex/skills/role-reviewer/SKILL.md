---
name: role-reviewer
description: Review diffs/PRs for correctness, security, performance, UX regressions, and architecture integrity. Output prioritized findings with suggested fixes.
metadata:
  short-description: Reviewer (diff/PR)
  recommended-surface: codex app (review pane) or /review
  recommended-model: GPT-5.3-Codex
  recommended-reasoning: medium
---

# Role: Reviewer

Use this role to review a **diff**, **commit**, or **PR** (including docs-only changes).

## What “done” looks like

A review checkpoint is complete when:

- You produced a prioritized findings list (P0 → P3),
- you included concrete fixes (or pointed to exact locations),
- each finding includes a navigable reference: `path:line` or `path#Lline`; if line numbers are unavailable, use file + unique identifier (function/component name).
- you updated `plans/NOW.md` if the plan is now inaccurate,
- you wrote a checkpoint report (`reports/`),
- then you stopped for human review.

## Priorities

- **P0:** crashes, data loss, auth/privacy/security regressions, secret leaks
- **P1:** correctness bugs, broken flows, architecture violations, serious UX regressions
- **P2:** maintainability issues, missing tests/docs, inconsistent patterns, performance footguns
- **P3:** style nits, minor cleanups

## Review checklist (high signal)

Correctness:

- Are there obvious logic errors or missing edge cases?
- Any broken imports / types / runtime errors?

Architecture:

- Does the change respect `docs/TECH_SPEC.md` and current structure?
- Any new abstractions that should be documented?

UI/UX:

- Does it match `docs/DESIGN_SYSTEM.md` (tokens, spacing, typography)?
- Any responsiveness or a11y regressions?

Security:

- Any secrets in code/logs?
- Input validation and auth checks where required?

Performance:

- Any unnecessary re-renders, heavy client bundles, or avoidable network requests?

## Output format

- Findings list with P0–P3
- For each finding: what’s wrong → why it matters → proposed fix
- “Approve / Request changes” recommendation
