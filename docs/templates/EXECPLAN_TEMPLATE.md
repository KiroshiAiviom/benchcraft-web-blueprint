# EXECPLAN.md (template)

One ExecPlan = one feature / bugfix / refactor.

Principles:

- Steps are **small** (checkpointable in ~15–30 minutes).
- Output is explicit.
- Completion is verifiable (checks + reviewable diff).
- Requirements come from product specs; do not invent.

## References (must be consistent with)

- Product spec(s): `docs/product-specs/<spec>.md`
- Design system: `docs/DESIGN_SYSTEM.md` (or `docs/templates/DESIGN_SYSTEM_TEMPLATE.md`)
- Technical decisions: `docs/TECH_SPEC.md` (or `docs/templates/TECH_SPEC_TEMPLATE.md`)
- Guardrails: `docs/QUALITY_SCORE.md`, `docs/SECURITY.md`, `docs/RELIABILITY.md`
- Optional decisions: `docs/design-docs/`

## Context

- What is being built?
- Why now?
- Constraints / assumptions:

## Plan steps (checkpointable)

Use stable step IDs (`S01`, `S02`, ...).
Each step should have a step sheet in `steps/`.

- [ ] S01 — <step title>
  - Step sheet: `steps/S01-<slug>.md`
  - Goal (one sentence):
  - Output (what exists after this step):
  - Checks (commands) or `N/A`:
  - Stop condition (what to show before continuing):

- [ ] S02 — <step title>
  - Step sheet: `steps/S02-<slug>.md`
  - Goal:
  - Output:
  - Checks:
  - Stop condition:

- [ ] S03 — <step title>
  - Step sheet: `steps/S03-<slug>.md`
  - Goal:
  - Output:
  - Checks:
  - Stop condition:

## Dependencies (approval-gated)

- Any new dependency? If yes, list it and mark: **requires approval**.

## Risks / unknowns

-  
