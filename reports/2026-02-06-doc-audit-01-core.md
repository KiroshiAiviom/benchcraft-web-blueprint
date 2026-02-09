# Doc Audit 01 — Core Bundle (2026-02-06)

Model: **GPT-5.3-Codex**  
Reasoning effort: **medium**

## /status

```txt
## main...origin/main
 M plans/NOW.md
?? reports/2026-02-06-doc-audit-01-core.md
```

## Scope (files reviewed)

- `AGENTS.md`
- `docs/WORKFLOW.md`
- `docs/SETUP.md`
- `docs/DOD.md`
- `docs/STACK_BASELINE.md`

## Quality gates

N/A (doc-audit checkpoint; no code changes).

## Findings (exactly 3 improvements)

### 1) Fix dependency-skill naming mismatch in `AGENTS.md`

What to change:
- Replace “Deps skill” with the actual skill name used in this repo (`role-deps`).

Why:
- The current wording is ambiguous and can cause the agent to miss the approval gate or use the wrong skill trigger.

Minimal suggested edit snippet (2–8 lines):

```diff
- - **No surprise deps.** Any new dependency requires explicit approval (use the Deps skill).
+ - **No surprise deps.** Any new dependency requires explicit approval (use the `role-deps` skill).
```

Impact:
- Reduces process mistakes around dependency/lockfile changes; improves instruction/tooling alignment.

Risk:
- Low. Purely clarifies terminology.

### 2) Remove/neutralize the hardcoded “GPT-5.2 Pro” planning recommendation in `docs/WORKFLOW.md`

What to change:
- Delete the specific external-model recommendation (or generalize to “separate planning session” without naming a model).

Why:
- This is likely to drift/outdate and conflicts with the repo’s “pinned model” guidance (GPT-5.3-Codex). Keeping model names out of workflow docs reduces churn.

Minimal suggested edit snippet (2–8 lines):

```diff
- Planning note: draft these docs during a separate planning session in ChatGPT (recommended: **GPT-5.2 Pro**) before you start Codex execution.
+ Planning note: draft these docs during a separate planning session before you start Codex execution.
```

Impact:
- Less time spent debating model choice; fewer future doc updates needed.

Risk:
- Low. Does not change the workflow, only removes a brittle recommendation.

### 3) De-duplicate baseline stack statements between `docs/SETUP.md` and `docs/STACK_BASELINE.md`

What to change:
- Replace the “stable baseline for:” bullets in `docs/SETUP.md` with a pointer to `docs/STACK_BASELINE.md`.

Why:
- The same baseline is described in two places today; any drift will confuse setup vs. expectations. A single canonical baseline doc keeps setup lean (and matches the workflow’s “keep docs lean” principle).

Minimal suggested edit snippet (2–8 lines):

```diff
-The goal is a stable baseline for:
-
-- Next.js (App Router) + TypeScript development
-- Bun-based installs and scripts
-- Codex-first, checkpoint-based iteration with reviewable diffs
+The goal is a stable baseline; see `docs/STACK_BASELINE.md` for the canonical stack/workflow baseline.
```

Impact:
- Fewer “which doc is right?” moments; cheaper maintenance for baseline updates.

Risk:
- Low. Only changes doc structure/ownership; no behavior change.

## Recommendation

Request changes (apply the 3 doc edits above).

## Commands run

- `git status -sb`
