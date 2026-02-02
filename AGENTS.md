# AGENTS.md — Benchcraft Web

You are an engineering agent operating inside a **Benchcraft Web** project.

## Goals

- Build production-grade **Next.js (App Router)** code in **TypeScript**.
- Keep changes small, reviewable, and auditable.
- Maintain a high UI quality bar using the project’s UI specs and tokens.

## Operating protocol (mandatory)

1) Read (in this order):

- `plans/NOW.md`
- `docs/DOD.md`
- `docs/UI_FOUNDATION_PACK.md`
- If present: `docs/STYLE_GUIDE.md` and `docs/UI_SPEC.md`

2) Execute **only the single next step** from `plans/NOW.md` / the active ExecPlan.

3) Work in **15–30 minute checkpoints**.

4) End every checkpoint with all of the following:

- A concise summary: what changed, why, what remains, and risks.
- A reviewable diff (or a file list + key snippets if a diff is not available).
- Run quality gates when available:
  - `lint`
  - `typecheck`
  - tests when the change is risky or user-facing
  - If the repository does not define scripts (e.g., no `package.json`), mark quality gates as `N/A` and explain why.
- Update the active plan (`plans/NOW.md` / ExecPlan checkboxes) to reflect reality.
- Write a checkpoint report in `reports/` (use `reports/TEMPLATE.md`).
- **Stop** and wait for user review.

## Constraints

- Do not commit, merge, rebase, or force-push unless explicitly instructed.
- Do not add/upgrade/remove dependencies without explicit approval. Before asking for approval:
  - explain why the dependency is needed,
  - list at least one alternative,
  - verify the API against current documentation when the usage is non-trivial.
- Treat `plans/NOW.md` as a structured session driver:
  - do not delete or reorder sections,
  - fill fields, toggle checkboxes, and keep it short.
- Avoid wrapper-only DOM nesting. Prefer layout primitives (Container/Section/Stack/Grid) and semantic HTML.
- If requirements are unclear, propose a plan update instead of guessing.

## UI quality bar

- Prefer design tokens (CSS variables) over hardcoded colors/spacing in components.
- Wire fonts via `next/font` and enforce typography tokens (font variables + a small type scale).
- Provide complete interaction states where applicable: hover, focus, active, disabled, loading, empty, error.
- Ensure keyboard navigation works and respect `prefers-reduced-motion`.
