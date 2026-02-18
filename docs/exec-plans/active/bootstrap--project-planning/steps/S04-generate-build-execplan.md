# S04 — Build ExecPlan (writes plan + switches NOW)

## Goal

Create the first build ExecPlan (checkpointable steps + step sheets) and switch NOW.md from planning to implementation.

## Expected output

- New plan folder under `docs/exec-plans/active/` with:
  - `EXECPLAN.md`
  - `steps/` step sheets
- `docs/exec-plans/active/NOW.md` updated to the new plan’s S01

## Files likely touched

- `docs/exec-plans/active/<new-plan>/EXECPLAN.md`
- `docs/exec-plans/active/<new-plan>/steps/*`
- `docs/exec-plans/active/NOW.md`
- `reports/*`

## Commands / checks

- N/A (planning-only)

## Stop condition

Stop after creating the plan, switching NOW.md, and writing a checkpoint report.

## Prompt reference

- Use: `docs/references/planning-prompts.md` (Prompt 4 — Build ExecPlan)
