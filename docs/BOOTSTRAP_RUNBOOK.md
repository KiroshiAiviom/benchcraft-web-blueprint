# Bootstrap Runbook (Empty Next App -> Agent-Ready Project)

This runbook is the canonical workflow for using this blueprint.

Goal:
- Keep this repository docs-only.
- Apply runtime/tooling setup in the target app repository only.

## Stage A - App + docs baseline

### Human runs

1. Create a fresh app:

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

2. Overlay blueprint assets into `my-app`:
- `AGENTS.md`
- `.codex/`
- `docs/`
- `reports/`
- (optional) `ARCHITECTURE.md`

### Agent does

1. Run docs bootstrap in the target repo:
- create `docs/TECH_SPEC.md` from template
- create `docs/DESIGN_SYSTEM.md` from template
- create first product spec in `docs/product-specs/`
2. Continue with normal checkpoint loop from `docs/exec-plans/active/NOW.md`.

Gate to complete Stage A:
- Canonical docs exist and are linked.
- No runtime/tooling files are added by default from this blueprint.

## Stage B - Full Bundle scaffolding (approved checkpoint)

Full Bundle:
- Playwright visual regression
- Stylelint mechanical token lint
- Chrome DevTools MCP

Dependency policy:
- Human approves and runs install commands.
- Agent does not edit dependencies before approval.

### Human runs (after approval)

In target repo:

```bash
bun add -d @playwright/test stylelint stylelint-config-standard
bunx playwright install
codex mcp add chrome-devtools -- npx chrome-devtools-mcp@latest
```

### Agent does (target repo only)

1. Add tooling files:
- `playwright.config.ts`
- `tests/visual/regression.spec.ts`
- `.stylelintrc.cjs`
- `.stylelintignore`
- `scripts/check-ui-token-drift.sh`
- `.github/workflows/ui-quality.yml` (if GitHub Actions is used)
2. Add scripts in `package.json`:
- `lint:styles`
- `lint:ui-tokens`
- `test:visual`
- `test:visual:update`
- `quality:ui`
3. Add/adjust ignores:
- `playwright-report`
- `test-results`

Gate to complete Stage B:
- Tooling files and scripts exist in target repo.
- Local runs are documented with command outputs.

## Stage C - Baselines + CI enforcement

### Human provides

1. Visual test base URL via CI/local env:
- `VISUAL_BASE_URL`
2. Initial critical routes (3-5 recommended):
- `VISUAL_ROUTES` (comma-separated, e.g. `/,/pricing,/dashboard`)

### Agent does

1. Configure route set and viewports for snapshots.
2. Generate initial baselines:

```bash
bun run test:visual:update
```

3. Run gates:

```bash
bun run lint:styles
bun run lint:ui-tokens
bun run test:visual
```

4. Wire CI variables and validate workflow behavior.

Gate to complete Stage C:
- Snapshot baseline exists for approved routes.
- CI gate executes lint + visual checks predictably.

## Human vs Agent responsibilities

Human:
1. Create target app repo.
2. Approve dependency additions.
3. Run dependency install and MCP setup commands.
4. Provide initial critical visual routes and target environment URL.

Agent:
1. Maintain blueprint docs and workflow contracts.
2. Scaffold Full Bundle files/scripts in target repo.
3. Configure and verify gates.
4. Report all commands and results in checkpoint output.

## Troubleshooting

### Snapshot flakiness

- Keep snapshots deterministic (stable data, stable fonts, stable viewport).
- Update baselines only when intentional UI changes are reviewed.
- Prefer a single stable CI environment for screenshot generation/comparison.

### Stylelint false positives

- Start with narrow disallowed rules (spacing/color drift only).
- Tune patterns per project conventions.
- Allow explicit exceptions only with review notes.

### Chrome DevTools MCP safety

- Use local/isolated browser profiles for debugging.
- Do not inspect sessions containing production secrets.
- Use MCP for diagnosis, not as a replacement for automated gates.

## Quick acceptance checks

1. Template repo contains docs/agent artifacts only.
2. README points to this runbook.
3. AGENTS references staged Full Bundle policy.
4. `docs/references/full-bundle-llms.txt` exists for command-level details.
