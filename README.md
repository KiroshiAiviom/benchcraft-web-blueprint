# Benchcraft Web Blueprint

A docs-first workflow blueprint for **Codex-first** development of production-grade **Next.js (App Router)** applications.

Designed to work best with the **Codex App** (threads, worktrees, reviewable diffs), while remaining compatible with the Codex IDE extension and CLI.

Default Codex model: **GPT-5.3-Codex** (reasoning effort: **medium**).

## Baseline stack

- Next.js (App Router) + React + TypeScript
- Bun (package manager + task runner)
- Tailwind CSS + shadcn/ui (component baseline)
- Biome (format/lint) + TypeScript typecheck

## What’s included

- `AGENTS.md` — concise operating rules (kept intentionally short).
- `ARCHITECTURE.md` — architecture map (keep it short; link out).
- `.codex/` — Codex configuration + skills (Planner, Builder, Refactor, Tests, UI).
- `docs/` — workflow/setup docs, guardrails, templates, and planning artifacts.
  - `docs/PLANS.md` — plan rules + structure
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

1) Bootstrap a new Next.js + Bun project (see `docs/SETUP.md`).
2) Overlay this blueprint into the project root.
3) Create and fill the canonical docs (above).
4) Drive each checkpoint from `docs/exec-plans/active/NOW.md` (one checkpoint per Codex thread).

## Key idea

**1 task → 1 checkpoint (15–30 min) → report → stop**.

Small diffs are what keep quality high and speed predictable.
