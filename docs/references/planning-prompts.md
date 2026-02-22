# Planning prompts (copy/paste)

These are short prompts you can paste into Codex to run the full planning loop inside the repo.

## Prompt 1 — Interrogation only (questions + answer sheet)

```text
Use role-planner.

Task: Run “Interrogation only” for this project.

Rules:
- If an Architecture/TA PDF is attached: read it first and extract facts.
- If a context dump transcript is provided: extract facts before asking questions.
- Source precedence: explicit user overrides > extracted Architecture/TA PDF facts > extracted context dump facts > targeted follow-up questions.
- Do NOT ask questions already answered by extracted inputs.
- Ask as many targeted questions as needed to eliminate uncertainty before development (50-100 is acceptable when needed).
- Continue questioning in follow-up rounds if required; do not force a fixed cap.
- Each question must be concrete and answerable (no vague brainstorming prompts).
- For most questions, provide 2–4 common options + “Other: ____”.
- Tag each question MUST / SHOULD / NICE.
- Provide an “Answer Sheet” at the end so I can reply quickly.
- Do NOT write or modify repo files in this step.
- Goal: resolve all material questions and uncertainties before development.
- If critical decisions remain unresolved after a question pass: report unresolved questions + assumptions in thread only and stop for answers.

Inputs I will provide:
- <project_seed> (use `docs/templates/PROJECT_SEED_TEMPLATE.md`)
- Context dump transcript (recommended)
- Architecture/TA PDF (optional)

Output format:
# 0) Inputs & precedence
# 0.5) Facts extracted from Architecture/TA PDF (only if attached)
# 0.6) Facts extracted from context dump (only if provided)
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
2) Extracted Architecture/TA PDF facts (if attached)
3) Extracted context dump facts (if provided)
4) My interrogation answers
5) Apply baseline defaults where defined (for example in `docs/templates/PROJECT_SEED_TEMPLATE.md` NFR defaults)
6) If still unknown and non-critical: write “TBD” and report unresolved items + assumptions in thread only (do not guess)
7) If still unknown and critical: stop and request answers before continuing

Deliverables (edit repo files):
- docs/product-specs/index.md
- 1–N specs in docs/product-specs/
- docs/DESIGN_SYSTEM.md
- docs/TECH_SPEC.md

Rules:
- Product Specs are the contract. No guessing.
- Keep cross-doc consistency: routes, feature IDs, terminology.
- Conflicts: don’t guess; mark TBD and report the conflict in thread only.

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
- If resolution requires human choice: do not guess; report unresolved decision(s) in thread only.

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
- For key-page UI work, include a variant-exploration step before implementation (5 variants for key pages, 3 for low-risk pages).
- No page UI build starts until variant selection is confirmed in thread.
- Update docs/exec-plans/active/NOW.md to point to the new plan’s S01.

Afterward:
- Move docs/exec-plans/active/bootstrap--project-planning to docs/exec-plans/completed/
- Write a checkpoint report in reports/
- STOP.
```

## Prompt 5 — UI variant exploration (docs-only, pre-build)

```text
Use role-ui.

Task: Generate page UI variants before implementation.

Inputs:
- Product spec sections for the page
- docs/DESIGN_SYSTEM.md (or template if not created yet)
- docs/DESIGN.md
- docs/FRONTEND.md
- docs/references/ui-taste-playbook-llms.txt

Rules:
- Create variants as docs-first outline blueprints (not code prototypes).
- Key page: generate 5 variants.
- Low-risk page: generate 3 variants.
- Copy `docs/templates/UI_PAGE_VARIANTS_TEMPLATE.md` into a page-specific artifact path:
  - `docs/ui-variants/<route-slug>-variants.md`
- Fill the copied page-specific file (do not edit the template file itself).
- Score each variant with rubric axes:
  - clarity of primary action
  - scanning speed
  - visual hierarchy
  - density balance
  - implementation risk
  - accessibility risk
- Do not implement UI in this step.
- Stop and wait for human-selected variant ID in thread.

Deliverables:
- Page-specific variant file (for example: `docs/ui-variants/<route-slug>-variants.md`) created from template
- Brief recommendation (best 1-2 options + tradeoffs)
- Explicit stop for human selection
```
