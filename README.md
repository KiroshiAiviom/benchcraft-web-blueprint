# Benchcraft Web Blueprint

A docs-first workflow blueprint for **Codex-first** development of production-grade **Next.js (App Router)** applications.

Designed to work best with the **Codex App** (threads, worktrees, reviewable diffs), while remaining compatible with the Codex IDE extension and CLI.

## Baseline stack

- Next.js (App Router) + React + TypeScript
- Bun (package manager + task runner)
- Tailwind CSS + shadcn/ui (component baseline)
- Biome (format/lint) + TypeScript typecheck

## What’s included

- `AGENTS.md` — concise operating rules (kept intentionally short).
- `ARCHITECTURE.md` — architecture map (keep it short; link out).
- `.codex/` — Codex configuration + skills (Planner, Builder, Refactor, Tests, UI).
- `docs/` — guardrails, templates, and planning artifacts.
  - `docs/PLANS.md` — plan structure + lifecycle
  - `docs/exec-plans/` — active/completed plans + tech debt tracker
  - `docs/product-specs/` — product specs (what + acceptance criteria)
  - `docs/design-docs/` — decision records + core beliefs
  - `docs/references/` — LLM-friendly tool references
  - `docs/QUALITY_SCORE.md` — quality rubric
  - `docs/DESIGN.md` + `docs/FRONTEND.md` — UI/UX + frontend defaults
  - `docs/SECURITY.md`, `docs/RELIABILITY.md`, `docs/PRODUCT_SENSE.md`
- `reports/` — checkpoint report template.
- `.github/` — PR template focused on quality gates and UI review.

## Canonical project docs (keep it lean)

For most projects, start with:

1) Product specs
   - `docs/product-specs/index.md`
   - at least one feature spec from `docs/product-specs/_TEMPLATE.md`

2) Design System
   - `docs/DESIGN_SYSTEM.md` from `docs/templates/DESIGN_SYSTEM_TEMPLATE.md`

3) Technical Spec
   - `docs/TECH_SPEC.md` from `docs/templates/TECH_SPEC_TEMPLATE.md`

Optional (high-value for enterprise):

- `docs/design-docs/` (decision records)
- `ARCHITECTURE.md` (short map; links to specs)

## How to use this blueprint

1) Start from an existing Next.js repo or create a new one (your preferred bootstrap).
2) Overlay this blueprint into the project root (docs + .codex + guardrails).
3) Run the first checkpoint:
   - open `docs/exec-plans/active/NOW.md`
   - execute the single checkbox (or use `.codex/skills/role-planner` to create a new plan)

## Key idea

**1 task → 1 checkpoint (15–30 min) → report → stop**.

Small diffs are what keep quality high and speed predictable.
