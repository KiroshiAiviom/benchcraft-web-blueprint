# Checkpoint Report — 2026-02-06 — Doc Audit 03 (Plans + Templates)

If a section does not apply, write `N/A`.

## Objective

- Doc-audit (plans + templates): propose exactly 3 improvements total (no rewrites).

## Surface + model

- Surface: Codex desktop app
- Worktree (if used): N/A
- Model + reasoning effort: GPT-5.3-Codex (medium)

## Summary (2–5 bullets)

- Reviewed planning + doc template scaffolding for ambiguity and workflow alignment.
- Found 3 high-leverage clarity issues that can cause agents to mis-execute (constraints, templates, and example code).

## Work performed

- Audited:
  - `plans/NOW.md`
  - `plans/WORK_QUEUE.md`
  - `reports/TEMPLATE.md`
  - `docs/templates/PRD_TEMPLATE.md`
  - `docs/templates/DESIGN_SYSTEM_TEMPLATE.md`
  - `docs/templates/TECH_SPEC_TEMPLATE.md`
  - `docs/templates/EXECPLAN_TEMPLATE.md`

## Findings (P0–P3) (optional)

Use for reviews/audits. For non-review checkpoints, write `N/A`.

- P0: N/A
- P1: N/A
- P2: `plans/NOW.md:34` and `plans/NOW.md:40` leave room for contradictory constraints.
  - What’s wrong: The objective says “propose 3 improvements per bundle” while the constraints section is empty, even though this checkpoint can have stricter rules (example given in the file).
  - Why it matters: Agents will follow the objective line and may miss checkpoint-specific constraints like “exactly 3 improvements total,” producing the wrong output format/quantity.
  - Proposed fix: When a checkpoint has special rules, fill `## Constraints` with the exact constraint text and mirror it in the objective (or remove the per-bundle wording).
- P2: `reports/TEMPLATE.md:36` makes doc-only audits slightly awkward to represent.
  - What’s wrong: The template has “Files changed” but no explicit place to record “Files reviewed/inspected” (common for doc-audits, investigations, and read-only checkpoints).
  - Why it matters: Audits can look incomplete if they have N/A diffs but meaningful inspected scope, and reviewers have to hunt for scope details in “Work performed.”
  - Proposed fix: Add a dedicated “Files reviewed/inspected” section (or rename/dual-purpose “Files changed” to cover both cases).
- P3: `docs/templates/DESIGN_SYSTEM_TEMPLATE.md:98` includes copy/paste examples that can accidentally become the project’s default.
  - What’s wrong: The “Implementation contract” contains ready-to-paste values (e.g., `ui-sans-serif`, Inter/Geist import) that are plausible defaults but can be adopted without an explicit, intentional typography decision.
  - Why it matters: It increases the chance of “template aesthetics” or an unintentional font choice becoming sticky early in a project.
  - Proposed fix: Replace “example skeleton” values with explicit placeholders (e.g., `<font-body>`, `<font-display>`) and/or add a one-line warning above the code blocks to prevent blind copy/paste.

## Recommendation (optional)

- N/A (doc-audit report)

## Files changed

- `plans/NOW.md`
- `reports/2026-02-06-doc-audit-03-templates.md`

## Commands run + results

- N/A (doc-only checkpoint)

## Definition of Done check

- Minimum checkpoint DoD: pass (report written; plan checkbox updated)
- UI DoD (if applicable): N/A (doc-only checkpoint)
- Dependency DoD (if applicable): N/A (doc-only checkpoint; no deps)

## Risks / open issues

- N/A

## Workflow / docs improvements (optional)

- N/A

## Next step suggestion

- N/A (per checkpoint rules: stop after report + plan update)

