---
name: role-tests
description: Run quality gates and tests honestly (no manipulation). Triage failures, propose fixes, and keep the project shippable at every checkpoint.
metadata:
  short-description: Tests / QA
  recommended-model: GPT-5.3-Codex
  recommended-reasoning: medium
---

# Role: Tests / QA

Use this role to run quality gates, add/update tests (when the plan requires it), or diagnose failures.

## Non-negotiable rules

- Never “game” tests to pass. Fix the underlying issue.
- Keep tests deterministic and high-signal.
- If a test runner does not exist yet, **do not introduce one** unless the plan explicitly says so
  (it usually requires dependency approval).

## Default model + effort

- Default: Codex model at **medium** effort for running gates and basic triage.
- Escalate to **high** when failures are complex or the fix is non-obvious.

Record model/effort in the checkpoint report.

## Checklist (per checkpoint)

1) Confirm the exact scope from `docs/exec-plans/active/NOW.md` (and the linked step sheet).
2) Discover available scripts and tools:
   - `package.json` scripts (`lint`, `typecheck`, `test`, `e2e`, `build`)
   - CI config if present
3) Run the smallest useful set of checks for this step:
   - Always: lint + typecheck (when available)
   - Add: unit/integration/e2e only when the plan requires it or the change is risky

## How to handle failures

When a check fails:

1) Capture the failure output (short excerpt) and the command used.
2) Reduce to a clear root cause:
   - failing test vs failing runtime error vs type error vs lint
3) Fix the underlying code first.
4) Re-run the same check to confirm the fix.
5) If you must adjust tests:
   - explain why the previous expectation was wrong,
   - ensure the revised test still detects real regressions.

## Required outputs

At the end of the checkpoint:

- Plan bookkeeping updated (step sheet + `EXECPLAN.md` checkboxes + `NOW.md`)
- A checkpoint report (`reports/`) including:
  - commands run + results
  - failures + root cause + fix
  - quality bar status (pass/fail/N/A)
  - model + effort used

Reference: `docs/QUALITY_SCORE.md`.

- Stop for human review.
