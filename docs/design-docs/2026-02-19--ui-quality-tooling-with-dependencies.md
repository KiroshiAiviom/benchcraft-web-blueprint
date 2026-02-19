# Design Doc - UI Quality Tooling (With Dependencies)

- Date: 2026-02-19
- Status: accepted
- Owner: team

## Decision

- Adopt a staged Full Bundle for target app repositories:
  - Playwright visual regression
  - Stylelint token-drift lint
  - Chrome DevTools MCP
- Keep this blueprint repository docs-only.
- Dependency changes remain human-approved and human-run.

## Context

- Manual checks alone were not enough to catch spacing drift and visual regressions.
- We need both prevention (lint) and detection (visual diffs), with tooling for faster diagnosis.
- The blueprint must stay lightweight and reusable across projects.

## Policy

1) Stage A: bootstrap app + canonical docs.
2) Stage B: apply Full Bundle scaffolding in target repo after dependency approval.
3) Stage C: establish baseline snapshots and enforce CI gates.

## Consequences

- Better UI consistency and earlier regression detection.
- More setup/maintenance overhead in target repos.
- Requires disciplined baseline and lint exception management.

## Risks and mitigations

- Snapshot flakiness: keep deterministic data/fonts/env and update baselines only for approved UI changes.
- Lint noise: start narrow, tune rules, require explicit exceptions.
- MCP safety: use isolated profiles and avoid sensitive sessions.

## Scope note

- This ADR applies to target app repositories, not this blueprint root.
- Operational details and commands are intentionally moved to:
  - `docs/BOOTSTRAP_RUNBOOK.md`
  - `docs/references/full-bundle-llms.txt`

## Links

- Related product spec: N/A
- Related ExecPlan: N/A
- Code/PR: N/A
