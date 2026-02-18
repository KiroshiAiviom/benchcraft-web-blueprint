# Plans

This repo is **checkpoint-driven**.
Plans live in the repo so the agent can work without relying on chat history.

## Where plans live

- Active plans: `docs/exec-plans/active/`
- Completed plans (archive): `docs/exec-plans/completed/`
- Tech debt tracker: `docs/exec-plans/tech-debt-tracker.md`

## The checkpoint driver

- `docs/exec-plans/active/NOW.md` is the single source of truth for the **current checkpoint thread**.
- It must contain **one objective** and **one next step**.

## ExecPlans (structure)

One ExecPlan = one feature / bugfix / refactor.

Each ExecPlan is a folder:

- `docs/exec-plans/active/<plan-slug>/EXECPLAN.md`
- `docs/exec-plans/active/<plan-slug>/steps/S01-...md`

Template(s):

- ExecPlan: `docs/templates/EXECPLAN_TEMPLATE.md`
- Step sheet: `docs/templates/STEP_SHEET_TEMPLATE.md`

Recommended naming:

- `YYYY-MM-DD--<slug>/` (keeps folders sorted)

## Agent-managed bookkeeping (recommended)

To reduce repetitive work, the agent is allowed to manage plan hygiene:

- create a plan folder when missing
- select the next step (first unchecked step)
- create/refresh the step sheet for the next checkpoint
- keep `NOW.md` aligned
- move finished plans to `completed/`

Use `.codex/skills/role-planner` when starting a new objective or when plans drift.

## Lifecycle

1) Create an ExecPlan folder under `active/` and fill `EXECPLAN.md`.
2) Drive one checkpoint from `active/NOW.md` by linking to a single step sheet.
3) After the checkpoint:
   - mark the step done in `EXECPLAN.md`
   - update the step sheet (status + results)
   - set the next step in `NOW.md` (only one)
4) When the plan is complete (all steps checked):
   - move the entire plan folder into `completed/`
   - set `NOW.md → Active ExecPlan` to `N/A`

## Keep plans lean

- Prefer links to specific sections (e.g., `docs/product-specs/<spec>.md#AC3`).
- Don’t paste long docs into plans.
- Unknowns become questions + assumptions in `NOW.md`, then stop for approval.
- Dependency changes must be marked **requires approval**.
