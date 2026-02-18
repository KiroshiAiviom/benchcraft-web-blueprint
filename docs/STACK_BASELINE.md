# Tech stack baseline (Benchcraft Web)

This document defines the default baseline used for most production web projects.

## Baseline (default)

- Framework: **Next.js** (App Router)
- Language: **TypeScript**
- Package manager / runner: **Bun**
- Styling: **Tailwind CSS**
- Component baseline: **shadcn/ui** (customized via project tokens)
- Format/lint: **Biome** (when applicable)
- Workflow: Codex-first checkpoints + PR-based review

## Quality gates (default expectations)

See `docs/QUALITY_SCORE.md` for checkpoint-level quality gates and when to run tests.

## Not fixed by this baseline (project-specific)

- Database (Postgres / Convex / etc.)
- ORM/query layer
- Authentication/authorization approach
- Deployment target (Vercel, internal infrastructure, customer-managed servers)
- E2E strategy (depends on project size and risk)

