---
name: role-planner
description: Maintain ExecPlans and step sheets: create plans, select the next step, keep NOW.md in sync, and archive completed plans.
---

# Role: Planner (ExecPlans)

Use this role to **reduce monotony** and keep execution unblocked:

- create an ExecPlan when one does not exist
- keep `docs/exec-plans/active/NOW.md` aligned with the plan
- create a short **step sheet** for the next checkpoint
- archive completed plans into `docs/exec-plans/completed/`

## Read-first (mandatory)

- `docs/PLANS.md` (plan rules + structure)
- `docs/exec-plans/active/NOW.md` (current objective + next step)
- `docs/QUALITY_SCORE.md` (quality bar)
- `docs/templates/NOW_TEMPLATE.md` (template reference; `active/NOW.md` must remain runnable)

If requirements are unclear:
- create/point to a product spec first: `docs/product-specs/PRODUCT_SPEC_TEMPLATE.md`
- record questions + assumptions in `NOW.md`, then stop

## Where plans live (structure)

An ExecPlan is a folder:

- `docs/exec-plans/active/<plan-slug>/EXECPLAN.md`
- `docs/exec-plans/active/<plan-slug>/steps/S01-...md`

Completed plans are moved to:

- `docs/exec-plans/completed/<plan-slug>/`

## What to do (algorithm)

### 1) Ensure a plan exists

If `NOW.md → Active ExecPlan` is `N/A` but there is a clear objective:

1) Create a new plan folder:
   - `docs/exec-plans/active/YYYY-MM-DD--<slug>/`
2) Create `EXECPLAN.md` from `docs/templates/EXECPLAN_TEMPLATE.md`.
3) If no product spec exists yet, propose creating one from:
   - `docs/product-specs/PRODUCT_SPEC_TEMPLATE.md`
   and stop (don’t invent requirements).

### 2) Select the next step

- If `NOW.md → Next step` is already defined and valid, keep it.
- Otherwise, pick the **first unchecked step** in the active ExecPlan.

### 3) Create/refresh the step sheet

For the chosen step:

1) Ensure a step sheet exists under `steps/` (use `docs/templates/STEP_SHEET_TEMPLATE.md`).
2) Fill it with:
   - goal (one sentence)
   - exact inputs (3–7 links max)
   - expected deliverables
   - checks (commands) or `N/A`
   - stop condition (what to show to the human)

### 4) Update NOW.md to drive the checkpoint

Update `docs/exec-plans/active/NOW.md` to include:

- objective (one sentence)
- link to the active ExecPlan folder
- a single next-step checkbox that references the step sheet
- a lean “Read first” list (prefer links to spec sections)

If `active/NOW.md` is missing or looks like a blank template stub, rewrite it using:

- `docs/templates/NOW_TEMPLATE.md`

Then fill it so it is **runnable** (one objective + one next-step checkbox).

### 5) After a step completes (bookkeeping)

When a step is finished:

- Mark the step checkbox in `EXECPLAN.md`.
- Update the step sheet status to `done` and summarize results.
- Update `NOW.md` to the next step (only one).

When the plan is complete (all steps checked):

- Move the entire plan folder to `docs/exec-plans/completed/`.
- In `NOW.md`, set:
  - `Active ExecPlan` → `N/A`
  - `Next step` → a single checkbox like “Define next objective / create next ExecPlan”.

## Dependency changes (approval-gated)

- Never edit `package.json` or lockfiles without explicit human approval.
- If a step requires deps, the step sheet must say **requires approval** and include exact commands for the human.
