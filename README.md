# Benchcraft Web Blueprint

A docs-first workflow blueprint for **Codex-first** development of production-grade **Next.js (App Router)** applications.

Designed to work best with the **Codex App** (threads, worktrees, reviewable diffs), while remaining compatible with the Codex IDE extension and CLI.

## Baseline stack

- Next.js (App Router) + React + TypeScript
- Bun (package manager + task runner)
- Tailwind CSS + shadcn/ui (component baseline)
- Biome (format/lint) + TypeScript typecheck

## What’s included

- `AGENTS.md` — concise operating rules for Codex.
- `.codex/` — Codex configuration + skills (Builder, Reviewer, Refactor, Tests, Deps, UI Foundation Pack).
- `docs/` — workflow + setup docs, UI Foundation Pack, and project templates.
- `plans/` — `WORK_QUEUE.md` (progress bridge) and `NOW.md` (drives each checkpoint).
- `reports/` — checkpoint report template.
- `.github/` — PR template focused on quality gates and UI review.

## Canonical project docs (keep it lean)

For most web apps, you only need three “source of truth” docs:

1) `docs/PRD.md` — scope, routes/flows, features + acceptance criteria.
2) `docs/DESIGN_SYSTEM.md` — typography, palette, tokens, layout primitives, component rules.
3) `docs/TECH_SPEC.md` — pinned stack, architecture, backend/data contracts, deployment notes.

Templates live in `docs/templates/`.

## How to use this blueprint

1) Bootstrap a new Next.js + Bun project (see `docs/SETUP.md`).
2) Overlay this blueprint into the project root.
3) Create and fill:
   - `docs/PRD.md`
   - `docs/DESIGN_SYSTEM.md`
   - `docs/TECH_SPEC.md`
4) Drive each checkpoint from `plans/NOW.md` (one checkpoint per Codex thread).

## Key idea

**1 task → 1 checkpoint (15–30 min) → report → stop**.

Small diffs are what keep quality high and speed predictable.
