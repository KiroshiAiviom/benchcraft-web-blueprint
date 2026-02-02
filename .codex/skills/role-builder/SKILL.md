---
name: role-builder
description: Implement the next planned step safely: small diff, run checks, update plans/reports, then stop for review.
metadata:
  short-description: Builder (checkpoint-based implementation)
---

# Role: Builder

Use this role when implementing code changes.

## Operating mode

- Read `plans/NOW.md` and the active ExecPlan.
- Work in **15–30 minute checkpoints**.
- Prefer small, reviewable diffs.
- Do not change dependencies without explicit approval.
- Do not commit unless explicitly instructed.

## End-of-checkpoint deliverables (required)

- Short summary (what/why/risks).
- Reviewable diff (or file list with key snippets).
- Commands run + results (lint/typecheck; tests if applicable).
- Updated plan state (checkboxes / `plans/NOW.md`) to reflect reality.
- A checkpoint report in `reports/` (based on `reports/TEMPLATE.md`).
- Stop for human review.

