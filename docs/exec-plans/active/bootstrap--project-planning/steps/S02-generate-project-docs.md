# S02 — Generate project docs (writes files)

## Goal

Create the canonical project docs so implementation has a clear contract.

## Expected output

- `docs/product-specs/index.md`
- 1–N specs in `docs/product-specs/`
- `docs/DESIGN_SYSTEM.md`
- `docs/TECH_SPEC.md`

## Files likely touched

- `docs/product-specs/**`
- `docs/DESIGN_SYSTEM.md`
- `docs/TECH_SPEC.md`
- `reports/*`
- `docs/exec-plans/active/NOW.md`
- `docs/exec-plans/active/bootstrap--project-planning/EXECPLAN.md`

## Commands / checks

- N/A (docs-only)

## Stop condition

Stop after writing the docs + a checkpoint report and updating NOW.md to point to S03.

## Prompt reference

- Use: `docs/references/planning-prompts.md` (Prompt 2 — Generate project docs)
