# Step Sheet — S01 — <title>

- Status: ready / in-progress / done / blocked
- Timebox: 15–30 minutes
- Plan: `../EXECPLAN.md`

## Goal (one sentence)

-

## Inputs (read first)

Keep this lean (3–7 links max). Prefer deep links (`#section`).

- 
- 

## Tasks (small + checkpointable)

- 
- 

## Dependency preflight (approval-gated, mandatory)

Before implementation, list all dependency requirements for this step.
If none are needed, write one row with `none`.

| Dependency | Why needed | Required by task bullet | Human-run command | Approval status |
|---|---|---|---|---|
|  |  |  |  | pending / approved / N/A |

Rule:
- If any required dependency is missing or unapproved, stop and request approval before implementation.

## UI variant preflight (when step includes page UI work)

Use this section for page-level UI implementation steps.
If not applicable, write `N/A`.

- Page classification: `key` / `low-risk` / `N/A`
- Required variant count: `5` / `3` / `N/A`
- Variant artifact path:
- Selected variant ID:
- Selection status: `confirmed in thread` / `pending` / `N/A`

## Commands (optional)

- 

## Expected deliverables (checklist)

- [ ] Reviewable diff (or file list + key snippets)
- [ ] Checkpoint report in `reports/`
- [ ] Quality gates run when available (`lint`, `typecheck`, tests if applicable) or `N/A`
- [ ] Plan bookkeeping updated (checkboxes + NOW.md)

## Stop condition

What should be shown to the human before continuing?

-
- If dependencies are missing/unapproved: stop with the dependency proposal + exact human-run command(s).
- If UI variant selection is required and status is `pending`: stop and request human choice before implementation.

## Notes / findings (optional)

-
