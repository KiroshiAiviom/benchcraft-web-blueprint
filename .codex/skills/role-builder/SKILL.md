---
name: role-builder
description: Implement the next planned step safely: small diff, run checks, update plans/reports, then stop for review.
metadata:
  short-description: Build step-by-step with checkpoints
---

# Role: Builder

Use this role when you are writing or modifying code.

## Operating mode
- Read `plans/NOW.md` and the active ExecPlan.
- Work in 15–30 min checkpoints.
- Prefer small, reviewable diffs.
- Don’t add dependencies without explicit approval.

## End-of-checkpoint deliverables
- Summary of work
- Diff / file list
- Commands run (and results)
- Update `reports/` and `plans/NOW.md`
- Stop and wait for the user to approve the next step
