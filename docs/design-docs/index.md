# Design docs

Design docs are short, durable **decision records**.
They exist to avoid re-litigating high-impact choices and to keep agent execution unblocked.

## When to write a design doc

Write a design doc when a decision is:

- high-impact (architecture, data model, auth, UI patterns)
- hard to reverse (migrations, vendor selection)
- cross-cutting (affects many areas)
- controversial (tradeoffs need to be recorded)

If it’s small or reversible, keep it in the ExecPlan step sheet instead.

## Where they live

- `docs/design-docs/` contains decision docs and long-lived beliefs.
- Keep docs **1–2 pages** and link to code/PRs.

Recommended naming:

- `YYYY-MM-DD--<slug>.md`

## Start here

- Core beliefs: `docs/design-docs/core-beliefs.md`
- Template: `docs/design-docs/_TEMPLATE.md`

## Index

Add new design docs here as they are created:

- `docs/design-docs/2026-02-19--ui-quality-tooling-with-dependencies.md` - accepted staged policy for Playwright visual diffs, Stylelint mechanical token linting, and Chrome DevTools MCP in target repos.
