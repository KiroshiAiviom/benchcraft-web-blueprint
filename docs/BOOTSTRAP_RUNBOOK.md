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
- `test:visual = playwright test tests/visual/regression.spec.ts`
- `test:visual:update = playwright test tests/visual/regression.spec.ts --update-snapshots`
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

1. Run Playwright preflight checklist:
   - dependencies installed (`@playwright/test`)
   - browser installed (`bunx playwright install` already completed)
   - `VISUAL_BASE_URL` is set and reachable
   - `VISUAL_ROUTES` is set with approved routes
2. Configure route set and viewports for snapshots.
3. Generate initial baselines:

```bash
bun run test:visual:update
```

4. Run gates:

```bash
bun run lint:styles
bun run lint:ui-tokens
bun run test:visual
```

5. Wire CI variables and validate workflow behavior.

Gate to complete Stage C:
- Snapshot baseline exists for approved routes.
- CI gate executes lint + visual checks predictably.

## Human vs Agent responsibilities

Human:
1. Create target app repo.
2. Approve dependency additions.
3. Run dependency install and MCP setup commands.
4. Provide initial critical visual routes and target environment URL.
5. Share the active local URL for browser/DevTools checks when needed.

Agent:
1. Maintain blueprint docs and workflow contracts.
2. Scaffold Full Bundle files/scripts in target repo.
3. Configure and verify gates.
4. Use `http://localhost:3000` by default for browser/DevTools checks (or explicit human override); do not stop/restart the human dev server unless explicitly asked.
5. Report all commands and results in checkpoint output.

## Dev Server Handshake (Chrome DevTools + localhost)

Default ownership:
- Human owns the active `bun dev` session.
- Default URL is `http://localhost:3000`.

Rules:
1. Agent should automatically use `http://localhost:3000` first.
2. Agent may verify `http://localhost:3000` from terminal before browser checks.
3. Do not auto-switch ports (for example 3000 -> 3001) unless the human explicitly asks.
4. Do not stop or restart the human's running dev server unless explicitly requested.
5. If `http://localhost:3000` is unavailable, report the check failure and ask for next action.

## Troubleshooting

### Visual tests failing (setup vs regression triage)

Treat failures in two buckets:

1. Setup/config failure (fix setup first):
   - `VISUAL_BASE_URL` missing/unreachable
   - `VISUAL_ROUTES` missing/empty
   - Playwright browser not installed
   - snapshot path/config mismatch
2. UI regression (product change):
   - diffs appear after setup is confirmed healthy
   - review and approve intentional updates, then run `bun run test:visual:update`

Quick checks:

```bash
echo "$VISUAL_BASE_URL"
echo "$VISUAL_ROUTES"
bunx playwright --version
bun run test:visual
```

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

1. Template repo contains docs and agent artifacts only.
2. README points to this runbook.
3. AGENTS references staged Full Bundle policy.
4. `docs/references/full-bundle-llms.txt` exists for command-level details.
