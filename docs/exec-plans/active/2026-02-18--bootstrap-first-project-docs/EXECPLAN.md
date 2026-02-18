# ExecPlan — Bootstrap first project docs

This plan exists so `docs/exec-plans/active/NOW.md` is always **runnable** even in a fresh template repo.

Goal: create the minimal set of **project-specific source-of-truth docs** needed for fast, high-quality, agent-driven development.

## References (must be consistent with)

- Product specs (contract):
  - `docs/product-specs/index.md`
  - `docs/product-specs/<spec>.md` (create at least one)
  - Template: `docs/product-specs/_TEMPLATE.md`
- Technical decisions:
  - `docs/TECH_SPEC.md` (or start from `docs/templates/TECH_SPEC_TEMPLATE.md`)
- Design system:
  - `docs/DESIGN_SYSTEM.md` (or start from `docs/templates/DESIGN_SYSTEM_TEMPLATE.md`)
- Guardrails:
  - `AGENTS.md`
  - `docs/QUALITY_SCORE.md`
  - `docs/SECURITY.md`, `docs/RELIABILITY.md`, `docs/PRODUCT_SENSE.md`

## Context

This repository is a blueprint/template.
Before real implementation work starts, create the minimum “contract docs” so the agent can execute without inventing requirements.

## Plan steps (checkpointable)

- [ ] S01 — Create minimal project docs (Product Spec + TECH_SPEC + DESIGN_SYSTEM)
  - Step sheet: `steps/S01-bootstrap-project-docs.md`
  - Goal (one sentence): establish the project’s written contract and pinned decisions.
  - Output (what exists after this step):
    - at least 1 Product Spec file under `docs/product-specs/`
    - `docs/TECH_SPEC.md` exists (initial pinned decisions)
    - `docs/DESIGN_SYSTEM.md` exists (initial tokens/primitives)
    - `docs/product-specs/index.md` links to the created spec(s)
  - Checks (commands) or `N/A`: `N/A` (docs-only)
  - Stop condition (what to show before continuing):
    - file list + 5–10 key bullets from each doc + open questions

## Dependencies (approval-gated)

- None.

## Risks / unknowns

- If requirements are unclear, record questions + assumptions in `docs/exec-plans/active/NOW.md` and stop.
