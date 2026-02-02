---
name: ui-foundation-pack
description: Build and polish professional Next.js + Tailwind + shadcn/ui interfaces with strong typography+palette, compact layout, smooth motion, and minimal DOM nesting. Inspired by high-end sites (Factory/Relume vibe) without copying.
metadata:
  short-description: Professional UI foundation + polish (Next.js/Tailwind)
---

# UI Foundation Pack (Benchcraft)

Use this skill when you are asked to:
- design or implement UI (pages/sections/components),
- polish UI/UX,
- fix spacing/alignment inconsistencies,
- choose typography / color palette / motion language,
- create a project-level style guide and tokens.

This skill is optimized for **Next.js (App Router) + TypeScript + Tailwind + shadcn/ui**.

---

## Core intent

We want UI that feels **professionally designed**, with:
- high **text/visual clarity**,
- **compact**, tidy composition (not “half-screen padding”),
- **distinctive** typography and palette (but not gaudy),
- subtle, high-impact **micro‑interactions** (smooth, 60fps),
- production-grade maintainability (clean component structure).

Avoid “AI‑generated aesthetics”:
- overused fonts (Inter/Roboto/Arial/system by default),
- clichéd purple gradients on white,
- generic hero layouts with predictable cards,
- random effects without a coherent direction.

---

## 0) Before you code: read the project’s UI truth

Always read (in this order):
1) `docs/UI_SPEC.md` if present (project-specific UI requirements)
2) `docs/STYLE_GUIDE.md` if present (fonts, palette, tokens)
3) `docs/UI_FOUNDATION_PACK.md` (this repo’s baseline)
4) Relevant existing components/styles in the codebase

If `STYLE_GUIDE.md` or `UI_SPEC.md` are missing, propose creating them (from templates) **before** implementing major UI.

---

## 1) Commit to a clear direction (professional, not cartoonish)

### 1.1 Identify constraints
- Audience: B2B enterprise / creator portfolio / hackathon demo
- Content density: low (marketing) vs high (dashboard)
- Performance budget: avoid heavy blur / huge images / JS-based animation everywhere
- A11y baseline: keyboard navigable, contrast, focus styles, reduced motion

### 1.2 Propose 2 “style directions”, then pick 1
Offer two distinct professional directions and recommend one. Examples:
- **Editorial Tech (dark)**: tight typography, subtle noise/texture, crisp borders, one accent, “factory-grade” vibe
- **Clean Studio (light)**: bright surfaces, elegant hover micro-interactions, airy but still compact
- **Industrial Utility**: utilitarian grid, restrained palette, strong hierarchy, purposeful motion
- **Minimal Luxe (no gold)**: refined neutrals, subtle depth, high-quality spacing and type

Do **not** copy any existing site. Use it only as inspiration for “quality bar”.

---

## 2) Design tokens first (so spacing/UX doesn’t drift)

Create/update tokens (CSS variables) for:
- Colors: bg/surface/text/muted/border/accent/accent-foreground
- Radii: e.g. 4/8/12 or a single base with variants
- Shadows: 0–2 levels only; crisp, not muddy
- Motion: duration + easing + stagger interval
- Spacing scale: base unit (4px) + named steps

Rules:
- Prefer **semantic tokens** over raw hex sprinkled everywhere.
- One accent color is usually enough (plus a “danger” if needed).
- If you introduce gradients: make them subtle, contextual, and consistent.

---

## 3) Typography: distinctive, readable, and consistent

Rules of thumb:
- Use **max 2 font families** (display + body).
- Choose a display font with character; body font must be calm and readable.
- Keep a tight scale: define H1/H2/H3/body/small with line-height and letter-spacing.
- Prefer variable fonts where possible.
- Establish defaults once (in STYLE_GUIDE) and reuse.

Avoid defaulting to Inter unless explicitly requested.

---



> Multilingual note: if the UI includes Cyrillic (or any non-Latin scripts), **verify font coverage** before committing.
> Prefer families with broad language support when needed (e.g., PT / Noto / IBM Plex families).


## 4) Layout & DOM discipline (solve the “nested div” pain)

Goal: minimal nesting, predictable spacing.

Rules:
- Use **layout primitives**:
  - `Container` (width + horizontal padding)
  - `Section` (vertical rhythm)
  - `Stack` (vertical spacing via gap)
  - `Cluster` (horizontal group, wraps)
  - `Grid` (responsive columns)
- Prefer `gap` for spacing between siblings; avoid padding-on-every-wrapper.
- Avoid “mystery wrappers”: if a wrapper exists, it must have a clear reason (layout, semantics, or styling).
- Use semantic tags (`section`, `header`, `nav`, `main`, `article`) where helpful.

If fixing spacing bugs:
- normalize paddings: pick one source of truth (Section/Container),
- remove redundant wrappers before tweaking tailwind classes.



### Debug protocol for spacing/alignment issues
1) Remove redundant wrappers.
2) Consolidate spacing into primitives (Section/Container/Stack/Grid).
3) Use temporary outlines/rings to see box boundaries.
4) Then polish.


---

## 5) Motion: fewer animations, higher impact

Principles:
- 60fps first: use `transform` and `opacity`.
- Prefer CSS transitions; use a motion library only when truly needed.
- “One orchestrated moment” > dozens of tiny animations:
  - a tasteful page-load stagger for hero,
  - 1–2 signature hover interactions (cards/buttons),
  - optional scroll reveal for key sections (respect reduced motion).

Always support `prefers-reduced-motion`.

---

## 6) Implementation style (Tailwind + shadcn/ui)

- Use shadcn components as the baseline, then customize via tokens and variants.
- Don’t fork everything — extend intentionally.
- Keep classnames readable:
  - extract complex UIs into components,
  - use `cn()` helper for conditional classes,
  - avoid one-line 200‑char class strings.

---

## 7) Output requirements (how you report)

When you finish a UI task, provide:
- What changed (short)
- Files changed
- What to visually verify manually (a checklist of 5–10 bullets)
- Risks / follow-ups (if any)

If you changed tokens/fonts/palette, explicitly call it out.

