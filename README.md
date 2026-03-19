# Benchcraft Web Blueprint

Benchcraft Web Blueprint is a docs-first, checkpoint-driven workflow for building production-oriented Next.js applications with Codex or similar coding agents.

The emphasis is not one-shot code generation. The emphasis is predictable planning, small reviewable diffs, docs as contracts, and explicit quality gates.

This repository is early-stage as a public open-source project. It is being packaged in public while the workflow continues to evolve.

## What this project is

- A reusable blueprint for agent-assisted web application work
- A structured planning and execution system for small checkpoints
- A set of templates, guardrails, and repo conventions for production-minded teams
- A Codex-first workflow that still stays readable without relying on chat history

## What this project is not

- A complete application starter with runtime code
- A claim of broad adoption or finished ecosystem status
- A replacement for product specs, engineering judgment, or human review

## Why it exists

Many AI-assisted app workflows fail in the same places:

- requirements get invented mid-build
- changes become too large to review comfortably
- docs drift away from implementation
- dependency changes slip in without clear approval
- teams cannot tell what the agent actually did

This blueprint tries to solve those problems with a simple operating model:

**1 task -> 1 checkpoint -> 1 report -> stop for review**

## Current status

- Public OSS baseline is being established now
- Public proof artifacts and examples are the next improvement area

This repository is intended to stand on its own public artifacts, documentation, and workflow clarity.

## What is included

- `AGENTS.md`
  Concise operating rules for the repository.
- `.codex/`
  Codex skills and environment configuration for planner, builder, tests, refactor, and UI roles.
- `docs/`
  Templates, planning artifacts, guardrails, and workflow references.
- `reports/`
  Checkpoint report template for traceable work.
- `ARCHITECTURE.md`
  A short architecture map that links deeper docs.

Important docs:

- `docs/PLANS.md` for ExecPlan lifecycle
- `docs/QUALITY_SCORE.md` for checkpoint quality expectations
- `docs/BOOTSTRAP_RUNBOOK.md` for staged setup in a target app repo
- `docs/SECURITY.md` and `docs/RELIABILITY.md` for baseline safety guardrails
- `docs/DESIGN.md` and `docs/FRONTEND.md` for UI/frontend defaults

## Baseline stack

The default baseline described by this blueprint is:

- Next.js App Router
- React
- TypeScript
- Bun
- Tailwind CSS
- Biome

Projects using the blueprint can diverge, but this is the default operating target today.

## How the workflow works

1. Product specs define what is being built and how success is evaluated.
2. ExecPlans turn that scope into checkpoint-sized steps.
3. `docs/exec-plans/active/NOW.md` holds the single active checkpoint.
4. Each checkpoint produces a small diff and a report, then stops for review.

The repository is designed to preserve project memory in files instead of relying on thread context alone.

## Quickstart

Use the staged setup in `docs/BOOTSTRAP_RUNBOOK.md`.

Minimal flow:

1. Create or open a Next.js project.
2. Overlay this blueprint into the project root.
3. Bootstrap the project docs.
4. Drive implementation through `docs/exec-plans/active/NOW.md`.

Example app creation:

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

## Who this is for

- Solo builders who want stronger process around AI-assisted work
- Small teams that care about reviewability and explicit scope control
- Maintainers experimenting with Codex-first or agent-assisted development workflows

## Who this is not for

- Teams looking for a full batteries-included app framework
- People who want the agent to bypass planning and review
- Projects that do not want repo-level process or documentation discipline

## Roadmap

Near-term public hardening:

- add sanitized public proof artifacts
- tighten examples and onboarding
- improve public OSS contribution surfaces

Longer-term:

- refine the workflow from real usage
- add more public examples and decision records
- make the blueprint easier for outside maintainers to adopt

## Contributing

Contributions are welcome, especially around documentation clarity, workflow sharpness, and public examples.

Start with:

- `CONTRIBUTING.md`
- `AGENTS.md`
- `docs/PLANS.md`

## License

MIT. See `LICENSE`.
