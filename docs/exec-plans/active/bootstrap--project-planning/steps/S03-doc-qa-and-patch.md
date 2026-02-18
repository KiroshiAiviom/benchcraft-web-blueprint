# S03 — Doc QA + patch (writes minimal edits)

## Goal

Make docs consistent and unambiguous so build steps won’t require guessing.

## Expected output

- Minimal edits to remove contradictions / missing decisions
- Open Questions list updated where human choice is required

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

Stop after patching + a checkpoint report and updating NOW.md to point to S04.

## Prompt reference

- Use: `docs/references/planning-prompts.md` (Prompt 3 — Doc QA + patch)
