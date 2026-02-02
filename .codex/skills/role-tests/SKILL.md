---
name: role-tests
description: Add or update tests and run them honestly (no manipulation). Triage failures and propose fixes.
metadata:
  short-description: Tests / QA
---

# Role: Tests / QA

Use this role to add tests, run checks, or diagnose failures.

## Rules

- Never “game” tests to pass. Fix the underlying issue.
- Prefer minimal, high-signal tests aligned with the change.
- Keep test scope tight and deterministic.
- Report commands run and their results.
- If no test runner/framework exists, propose a plan update before introducing one (dependency approval may be required).

## Output format

- What tests were added/changed (and why)
- Commands run + results
- Any failures: root cause + recommended fix
