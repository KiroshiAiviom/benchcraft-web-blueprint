# Benchcraft Web Blueprint (docs-first)

A docs-first workflow blueprint for **Codex-first** development of production-grade **Next.js (App Router)** applications.

This blueprint is designed to work best with the **Codex app** (threads, worktrees, built-in diff review),
while staying compatible with the Codex IDE extension and CLI.

## Baseline stack

- Next.js (App Router) + React + TypeScript
- Bun (package manager + task runner)
- Tailwind CSS + shadcn/ui (component baseline)
- Biome (format/lint) + TypeScript typecheck

## What’s included

- `AGENTS.md` — concise operating rules for Codex.
- `.codex/` — project Codex configuration + skills.
- `docs/` — workflow documentation, UI Foundation Pack, and templates (BRIEF/UI_SPEC/STYLE_GUIDE/etc.).
- `plans/` — `WORK_QUEUE.md` and `NOW.md` (drives every checkpoint).
- `reports/` — checkpoint report template.
- `.github/` — PR template focused on quality gates and UI review.

## How to use this blueprint

1) Create a new Next.js project (see `docs/PROJECT_BOOTSTRAP.md`).
2) Copy this repository into that project root (overlay).
3) Open the project in the **Codex app** and configure Local Environments (setup script + actions).
4) Fill project docs using templates:
   - `docs/BRIEF.md`
   - `docs/UI_SPEC.md`
   - `docs/STYLE_GUIDE.md`
5) Drive each checkpoint from `plans/NOW.md` (one checkpoint per thread).

## Key idea

**1 task → 1 checkpoint (15–30 min) → report → stop**.

Small diffs are what keep quality high and speed predictable.
