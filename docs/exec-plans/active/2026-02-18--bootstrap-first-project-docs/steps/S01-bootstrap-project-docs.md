# Step Sheet — S01 — Bootstrap project docs

- Status: ready
- Timebox: 15–30 minutes
- Plan: `../EXECPLAN.md`

## Goal (one sentence)

Create the minimal project docs (Product Spec + TECH_SPEC + DESIGN_SYSTEM) so implementation work does not invent requirements or stack decisions.

## Inputs (read first)

- `AGENTS.md`
- `docs/QUALITY_SCORE.md`
- `docs/product-specs/_TEMPLATE.md`
- `docs/product-specs/index.md`
- `docs/templates/TECH_SPEC_TEMPLATE.md`
- `docs/templates/DESIGN_SYSTEM_TEMPLATE.md`

## Tasks (small + checkpointable)

1) **Create at least one Product Spec**
   - Create a file: `docs/product-specs/<your-first-slice>.md`
   - Use `docs/product-specs/_TEMPLATE.md` as the starting point.
   - Keep it lean: goal, scope, acceptance criteria, non-goals, open questions.

2) **Update the Product Spec index**
   - Add the new spec to `docs/product-specs/index.md`.

3) **Create pinned decisions docs** (minimal v0)
   - Create `docs/TECH_SPEC.md` from `docs/templates/TECH_SPEC_TEMPLATE.md`.
   - Create `docs/DESIGN_SYSTEM.md` from `docs/templates/DESIGN_SYSTEM_TEMPLATE.md`.
   - If you don’t know something yet, write `TBD` plus the decision owner/question.

4) **Update NOW.md to reflect reality**
   - In `docs/exec-plans/active/NOW.md`, update:
     - `Read first` to point to the created docs
     - objective if it changed
     - keep next step as this S01 until done

5) **Write a checkpoint report** in `reports/`
   - Summarize what docs were created and what remains unclear.
   - If there are open questions that block implementation, list them and **stop**.

## Commands (optional)

- `N/A` (docs-only)

## Expected deliverables (checklist)

- [ ] At least one Product Spec exists under `docs/product-specs/`
- [ ] `docs/product-specs/index.md` updated with links
- [ ] `docs/TECH_SPEC.md` created (v0)
- [ ] `docs/DESIGN_SYSTEM.md` created (v0)
- [ ] Checkpoint report in `reports/`
- [ ] Plan bookkeeping updated (checkboxes + NOW.md)

## Stop condition

Show:

- list of created/updated files
- top 5–10 bullets from each doc (so the human can verify direction)
- the list of open questions (if any)

Then stop for human review.
