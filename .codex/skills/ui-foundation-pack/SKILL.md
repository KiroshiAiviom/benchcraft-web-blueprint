---
name: ui-foundation-pack
description: Create distinctive, production-grade UI for Next.js + Tailwind + shadcn/ui using strong typography, cohesive tokens, compact layout, deliberate motion, and minimal DOM nesting.
metadata:
  short-description: UI foundation + polish (Next.js/Tailwind)
---

# UI Foundation Pack (skill)

Use this skill when you are asked to:
- design or implement UI (pages/sections/components),
- polish UI/UX,
- fix spacing/alignment inconsistencies,
- define typography, palette, tokens, or motion conventions.

Baseline target: **Next.js (App Router) + TypeScript + Tailwind + shadcn/ui**.

## Read-first order (do not skip)

1) `docs/UI_SPEC.md` (project-specific UI requirements), if present  
2) `docs/STYLE_GUIDE.md` (typography, palette, tokens), if present  
3) `docs/UI_FOUNDATION_PACK.md` (this repo’s baseline)  
4) Existing UI components and styles in the codebase

If `STYLE_GUIDE.md` or `UI_SPEC.md` is missing and the UI scope is non-trivial, propose creating/filling it (from templates) before major UI work.

## Operating principles

- Commit to a clear direction (tone, density, signature element). Avoid “generic template UI”.
- Establish tokens early. Use semantic tokens (CSS variables) and map them in Tailwind.
- Keep layouts compact and readable. Avoid excessive empty space.
- Keep motion deliberate and performance-friendly (transform/opacity; reduced motion support).
- Keep DOM shallow. Prefer semantic HTML and reusable layout primitives.

## Execution recipe

1) Propose **two** viable style directions (name + 5 bullets each), then recommend one.
2) Define or update **typography + palette + tokens** (in `docs/STYLE_GUIDE.md`).
3) Implement UI in small checkpoints:
   - build primitives first (Container/Section/Stack/Grid),
   - then core components,
   - then polish (states, motion, details).
4) Validate with the UI QA checklist in `docs/UI_FOUNDATION_PACK.md`.
5) End with diff + short manual verification checklist.

## Spacing/alignment debugging protocol

When spacing feels inconsistent:
- remove wrapper-only nodes,
- re-establish a single spacing source of truth (`gap` on parents; one padding layer inside cards),
- use temporary debug outlines,
- only then adjust cosmetics.

## Output requirements

- Clear direction summary (chosen style direction and why)
- Tokens/typography changes recorded in `docs/STYLE_GUIDE.md` when applicable
- Reviewable diff + list of manual UI checks (desktop/mobile, focus, reduced motion)

