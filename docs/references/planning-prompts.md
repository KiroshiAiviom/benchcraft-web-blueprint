# Planning prompts (copy/paste)

These are short prompts you can paste into Codex to run the full planning loop inside the repo.

## Prompt 1 — Interrogation only (questions + answer sheet)

```text
Use role-planner.

Task: Run “Interrogation only” for this project.

Rules:
- If a Technical Assignment (TA) PDF is attached: read it first and extract facts.
- Do NOT ask questions already answered by the TA.
- Ask 35–55 questions in ONE pass, grouped by category.
- Each question must be concrete and answerable.
- For most questions, provide 2–4 common options + “Other: ____”.
- Tag each question MUST / SHOULD / NICE.
- Provide an “Answer Sheet” at the end so I can reply quickly.
- Do NOT write or modify repo files in this step.

Inputs I will provide:
- <project_seed>
- TA PDF (optional)

Output format:
# 0) Inputs & precedence
# 0.5) Facts extracted from TA (only if TA attached)
# 1) Understanding snapshot (max 6 bullets)
# 2) Assumption ledger (table)
# 3) Questions (grouped)
# 4) Answer Sheet (copy/paste)
```

## Prompt 2 — Generate project docs (writes files)

```text
Use role-planner.

Task: Generate project-specific canonical docs from my answers.

Source precedence:
1) Explicit overrides in my message
2) TA facts (if attached)
3) My interrogation answers
4) If still unknown: write “TBD” + add to Open Questions (do not guess)

Deliverables (edit repo files):
- docs/product-specs/index.md
- 1–N specs in docs/product-specs/
- docs/DESIGN_SYSTEM.md
- docs/TECH_SPEC.md

Rules:
- Product Specs are the contract. No guessing.
- Keep cross-doc consistency: routes, feature IDs, terminology.
- Conflicts: don’t guess; mark TBD + note the conflict.

After writing:
- Create a checkpoint report in reports/.
- Update bootstrap ExecPlan checkboxes (S02).
- Update docs/exec-plans/active/NOW.md to point to S03.
- STOP.
```

## Prompt 3 — Doc QA + patch (writes minimal edits)

```text
Use role-planner.

Task: Doc QA — fix docs so implementation won’t require guessing.

Scope:
- docs/product-specs/**
- docs/DESIGN_SYSTEM.md
- docs/TECH_SPEC.md

Rules:
- Identify the top 3 contradictions / missing decisions that would block or mislead build.
- Apply minimal edits directly to resolve them.
- If resolution requires human choice: add an Open Question (do not guess).

After patching:
- Write a checkpoint report in reports/.
- Update bootstrap ExecPlan checkboxes (S03).
- Update docs/exec-plans/active/NOW.md to point to S04.
- STOP.
```

## Prompt 4 — Build ExecPlan (writes plan + switches NOW)

```text
Use role-planner.

Task: Create the first build ExecPlan and switch NOW.md to implementation.

Inputs:
- docs/product-specs/**
- docs/DESIGN_SYSTEM.md
- docs/TECH_SPEC.md
- Guardrails: docs/QUALITY_SCORE.md + SECURITY/RELIABILITY/PRODUCT_SENSE

Rules:
- Steps must be checkpointable (15–30 min) and reference feature IDs/routes.
- Each step must have a step sheet: goal, expected output, files, checks (or N/A), stop condition.
- Update docs/exec-plans/active/NOW.md to point to the new plan’s S01.

Afterward:
- Move docs/exec-plans/active/bootstrap--project-planning to docs/exec-plans/completed/
- Write a checkpoint report in reports/
- STOP.
```
