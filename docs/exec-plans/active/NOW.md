# NOW.md (checkpoint driver)

This file is the single source of truth for the **current checkpoint thread**.

Rules:

- Keep this file short and high-signal.
- **Do not delete sections or headings.** If something does not apply, write `N/A` and a 1-line reason.
- Only one objective and one next step at a time.

## Read first (context files)

List **only what is needed** for this checkpoint.

Guidelines:

- Aim for **3–7 files** max.
- Prefer a pointer to a specific section (e.g., `docs/product-specs/foo.md#AC3`) over loading an entire long doc.
- If a file does not exist yet, link its template (don’t paste the template content into this file).

Baseline:

- `docs/QUALITY_SCORE.md`

Add as needed:

- Product spec(s): `docs/product-specs/index.md` + `docs/product-specs/<spec>.md`
  - (or start from `docs/product-specs/_TEMPLATE.md`)
- Technical decisions: `docs/TECH_SPEC.md` (or `docs/templates/TECH_SPEC_TEMPLATE.md`)
- Design system: `docs/DESIGN_SYSTEM.md` (or `docs/templates/DESIGN_SYSTEM_TEMPLATE.md`)
- Design beliefs/decisions: `docs/design-docs/core-beliefs.md` (and relevant design doc links)
- UI work: `docs/DESIGN.md` + `docs/FRONTEND.md`
- key code files / routes relevant to the step

## Session settings (optional)

- Surface:
- Worktree (if used):
- Model: **GPT-5.3-Codex** (default; pinned in `.codex/config.toml`)
- Reasoning effort: **medium** by default; use **high** when stuck; use **xhigh** for the hardest tasks

## Current objective (one sentence)

- 

## Active ExecPlan

- (link to a plan folder under `docs/exec-plans/active/` or write `N/A`)

## Constraints (checkpoint-specific, optional)

If this checkpoint has special constraints (e.g., “exactly 3 improvements”, “docs-only”, “no new deps”), list them here.

- Expected outputs:
- Allowed edits:
- Prohibited:

## Next step (only one)

- [ ] …

### Timebox

- 15–30 minutes

### Expected deliverables at checkpoint end (checklist)

- [ ] Reviewable diff (or a file list + key snippets)
      If this is a read-only checkpoint, write `N/A` and summarize the inspected scope.
- [ ] Checkpoint report in `reports/`
- [ ] Quality gates run **when available** (`lint`, `typecheck`, tests if applicable)
      If no scripts exist (e.g., no `package.json`), mark `N/A` and state why.
- [ ] Plan updated to reflect reality (checkboxes / next step / step sheet)
- [ ] Stop for human review

## Parking lot (optional)

Use this for ideas or follow-ups that are **not part of the current step**.

- 
