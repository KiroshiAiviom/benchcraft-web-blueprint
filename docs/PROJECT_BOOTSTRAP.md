# Project bootstrap (from blueprint to a Next.js project)

This document describes how to apply this blueprint to a new Next.js codebase.

## 1) Create a new project (Next.js + Bun)

```bash
bun create next-app@latest my-app \
  --typescript \
  --tailwind \
  --biome \
  --app \
  --src-dir \
  --import-alias "@/*" \
  --use-bun \
  --empty
```

Then:

```bash
cd my-app
bun install
```

## 2) Confirm project scripts

Bun recommends prefixing Next commands via `bun --bun next ...` when running Next.js on Bun.

Ensure `package.json` scripts are correct for your setup, e.g.:

```jsonc
{
  "scripts": {
    "dev": "bun --bun next dev",
    "build": "bun --bun next build",
    "start": "bun --bun next start",
    "lint": "biome check .",
    "format": "biome format --write .",
    "typecheck": "tsc --noEmit"
  }
}
```

## 3) Apply the blueprint overlay

Copy the following into the project root:

- `AGENTS.md`
- `.codex/`
- `docs/`
- `plans/`
- `reports/`
- `.github/` (recommended)

## 4) Initialize project docs (before major implementation)

Create and fill these files using templates:

- `docs/BRIEF.md` (from `docs/templates/BRIEF_TEMPLATE.md`)
- `docs/UI_SPEC.md` (from `docs/templates/UI_SPEC_TEMPLATE.md`)
- `docs/STYLE_GUIDE.md` (from `docs/templates/STYLE_GUIDE_TEMPLATE.md`)
- `docs/ARCHITECTURE.md` (from `docs/templates/ARCHITECTURE_TEMPLATE.md`) when non-trivial

## 5) Run the workflow

- Update `plans/WORK_QUEUE.md` with top-level tasks.
- Set the current session objective in `plans/NOW.md`.
- Run Codex in checkpoint mode (15–30 min), then review diffs and iterate.
