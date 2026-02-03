---
name: ui-foundation-pack
description: Create distinctive, production-grade UI for Next.js + Tailwind + shadcn/ui using strong typography, cohesive tokens, compact layout, deliberate motion, and minimal DOM nesting.
metadata:
  short-description: UI foundation + polish (Next.js/Tailwind)
  recommended-model: gpt-5.2-codex
  recommended-reasoning: medium
---

# Skill: UI Foundation Pack

Use this skill when you are asked to:

- design or implement UI (pages/sections/components),
- polish UI/UX and visual clarity,
- fix spacing/alignment inconsistencies,
- define typography, palette, tokens, or motion conventions.

Baseline target: **Next.js (App Router) + TypeScript + Tailwind + shadcn/ui**.

## Default model + effort

- Default: Codex model at **medium** effort (fast iteration with good quality).
- Escalate to **high** for complex UI flows, design-system changes, or difficult UX bugs.
- Record model/effort in the checkpoint report.

## Read-first order (do not skip)

1) `docs/UI_SPEC.md` (what the UI must do), if present  
2) `docs/STYLE_GUIDE.md` (typography/palette/tokens/motion), if present  
3) `docs/UI_FOUNDATION_PACK.md` (constraints + contracts)  
4) Existing UI components and styles in the codebase

If `STYLE_GUIDE.md` or `UI_SPEC.md` is missing and the UI scope is non-trivial, propose creating/filling it (from templates) **before** major UI work.

## Design intent rules (high leverage)

- Do not copy reference sites. Use them only for inspiration (interaction patterns, typographic discipline, density).
- Avoid “AI-generated aesthetics”:
  - default font stacks used everywhere,
  - generic gradient washes,
  - random glow/blur/noise without a coherent system,
  - animation on every element.
- Aim for a professional look:
  - strong typography and spacing rhythm,
  - cohesive palette,
  - compact, tidy composition,
  - 1–2 signature moments (not a dozen micro-animations).

## Execution recipe (repeatable)

### A) Direction (when style is not locked)

1) Propose **two** viable style directions:
   - name + 5 bullets each (typography, palette intent, density, signature moment, do/don’t)
2) Recommend one and explain why (1–2 sentences).
3) Update `docs/STYLE_GUIDE.md` with the selected direction.

### B) Tokens first (enforceable)

- Typography:
  - `next/font` → CSS variables (`--font-body`, `--font-display`)
  - small, tokenized type scale (H1/H2/H3/body/sm + leading + tracking)
- Palette:
  - semantic tokens (shadcn-compatible)
  - avoid one-off hex values
- Motion:
  - durations + easing tokens
  - reduced-motion policy and patterns

### C) Layout primitives → components → polish

Implement in this order:

1) Layout primitives (Container/Section/Stack/Grid)
2) Core components (Button/Input/Card/etc.)
3) Product/section composition (screens/sections)
4) Polish:
   - interaction states (hover/focus/active/disabled/loading/empty/error)
   - motion (motion-safe + motion-reduce)
   - alignment and spacing consistency

### D) QA

Validate with the checklist in `docs/UI_FOUNDATION_PACK.md`:

- visual hierarchy + text clarity
- spacing consistency (same components use the same padding/gaps)
- focus-visible + keyboard navigation
- reduced motion
- responsive layout across 2–3 breakpoints
- performance sanity (avoid heavy effects; prefer transform/opacity)

## Spacing/alignment debugging protocol

When spacing feels inconsistent:

1) Remove wrapper-only nodes.
2) Re-establish a single spacing source of truth:
   - between blocks → `gap` on the parent
   - inside cards → one padding layer
3) Use temporary debug outlines (`ring-1`/`outline`) in dev-only mode.
4) Only then adjust cosmetics (shadows, gradients, borders).

## Required outputs (per checkpoint)

At the end of each UI checkpoint:

- `plans/NOW.md` updated (checkboxes reflect reality)
- reviewable diff (or file list + key snippets)
- gates run when available (`lint`, `typecheck`; tests when applicable)
- checkpoint report in `reports/` including:
  - direction/tokens decisions (if any)
  - manual UI checks performed (desktop + mobile, focus, reduced motion)
  - model + effort used
- stop for human review
