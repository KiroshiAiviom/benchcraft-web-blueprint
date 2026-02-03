# NOW.md (session driver)

This file is the single source of truth for the **current Codex session**.

Rules:

- Keep this file short and high-signal.
- **Do not delete sections or headings.** If something does not apply, write `N/A` and a 1-line reason.
- Only one objective and one next step at a time.

## Read first (context files)

- `docs/BRIEF.md` (or `docs/templates/BRIEF_TEMPLATE.md`)
- `docs/UI_SPEC.md` (or `docs/templates/UI_SPEC_TEMPLATE.md`)
- `docs/STYLE_GUIDE.md` (or `docs/templates/STYLE_GUIDE_TEMPLATE.md`)
- `docs/DOD.md`
- `docs/UI_FOUNDATION_PACK.md`
- `plans/WORK_QUEUE.md`

## Session settings (optional)

- Surface:  
- Worktree (if used):  
- Model + reasoning effort:  

## Current objective (one sentence)

-  

## Active ExecPlan

- (link to `docs/EXECPLAN-*.md` or similar)

## Next step (only one)

- [ ]  

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
