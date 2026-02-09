# NOW.md (session driver)

This file is the single source of truth for the **current Codex session**.

Rules:

- Keep this file short and high-signal.
- **Do not delete sections or headings.** If something does not apply, write `N/A` and a 1-line reason.
- Only one objective and one next step at a time.

## Read first (context files)

Always:

- `docs/PRD.md` (or `docs/templates/PRD_TEMPLATE.md`)
- `docs/DESIGN_SYSTEM.md` (or `docs/templates/DESIGN_SYSTEM_TEMPLATE.md`)
- `docs/TECH_SPEC.md` (or `docs/templates/TECH_SPEC_TEMPLATE.md`)
- `docs/DOD.md`
- `plans/WORK_QUEUE.md`

If this checkpoint touches UI:

- `docs/UI_FOUNDATION_PACK.md`

## Session settings (optional)

- Surface:
- Worktree (if used):
- Model: **GPT-5.3-Codex** (default; pinned in `.codex/config.toml`)
- Reasoning effort: **medium** by default; use **high** when stuck; use **xhigh** for the hardest tasks

## Current objective (one sentence)

- Codex doc-audit run: propose 3 improvements per bundle (no rewrites).

## Active ExecPlan

- (link to `plans/EXECPLAN-*.md` or `docs/EXECPLAN-*.md`)

## Constraints (checkpoint-specific, optional)

If this checkpoint has special constraints (e.g., “exactly 3 improvements”, “docs-only”, “no new deps”), list them here.

- Expected outputs:
- Allowed edits:
- Prohibited:

## Next step (only one)

- [ ] DOC-AUDIT 01 — Core docs

### Timebox

- 15–30 minutes

### Expected deliverables at checkpoint end (checklist)

- [ ] Reviewable diff (or a file list + key snippets)
      If this is a read-only checkpoint, write `N/A` and summarize the inspected scope.
- [ ] Checkpoint report in `reports/`
- [ ] Quality gates run **when available** (`lint`, `typecheck`, tests if applicable)
      If no scripts exist (e.g., no `package.json`), mark `N/A` and state why.
- [ ] Plan updated to reflect reality (checkboxes / next step)
- [ ] Stop for human review
