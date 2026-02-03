# UI Foundation Pack (Benchcraft Web)

A shared baseline for building **distinctive, production-grade** UI across Benchcraft web projects.

This is not a component library. It is a set of **constraints, tokens, primitives, and QA checks**
that keeps interfaces professional and consistent without making projects look identical.

---

## 1) Principles

- **Typography-first.** The interface should feel designed even before color and motion.
- **Cohesive palette.** Neutrals + one strong accent beats “many timid accents”.
- **Compact, tidy composition.** Avoid “half-screen padding”; keep rhythm and density intentional.
- **Intentional motion.** A few high-impact moments beat many small, noisy animations.
- **Clarity over decoration.** Visual details must support hierarchy and usability.
- **Maintainability.** Minimal DOM nesting, reusable primitives, tokens over hardcoded values.

---

## 2) Anti-patterns

Avoid these by default:

- Generic landing patterns: predictable hero + feature cards + gradient wash.
- Random effects (glow/blur/noise) without a coherent direction.
- “Motion everywhere” (especially JS-driven animation for simple interactions).
- Wrapper-only DOM nesting (deep `<div>` stacks with padding on every layer).
- Fixing spacing problems by adding more spacing instead of simplifying structure.

---

## 3) Typography

### 3.1 Rules

- Use **max 2 font families**: a display face + a body face.
- Define a **small type scale** and stick to it:
  - H1 / H2 / H3 / body / small (+ line-height + letter-spacing)
- Prefer variable fonts where possible.
- Ensure language coverage (Cyrillic/extended Latin/etc.) before committing.

### 3.2 Quick shortlist (display + body pairs)

Use these as a starting point. Avoid converging on the same pair across projects.

- IBM Plex Sans (body) + IBM Plex Serif (display)
- Source Sans 3 (body) + Source Serif 4 (display)
- Fira Sans (body) + Alegreya (display)
- PT Sans (body) + PT Serif (display) — strong Cyrillic support
- Noto Sans (body) + Noto Serif (display) — broad language support
- Manrope (body) + Spectral (display)

### 3.3 Typography tokens + implementation contract

**Contract:** typography is defined in tokens. Components do not invent ad-hoc sizes, line-heights,
or letter-spacing.

**Minimum token set**

Fonts:

- `--font-body` (CSS variable set by `next/font`)
- `--font-display` (CSS variable set by `next/font`)

Scale (example names; tune values per project):

- `--text-h1`, `--leading-h1`, `--tracking-h1`
- `--text-h2`, `--leading-h2`, `--tracking-h2`
- `--text-h3`, `--leading-h3`, `--tracking-h3`
- `--text-body`, `--leading-body`, `--tracking-body`
- `--text-sm`, `--leading-sm`, `--tracking-sm`

**Next.js `next/font` wiring (example)**

```ts
// src/app/fonts.ts
import { Inter, Fraunces } from "next/font/google";

export const fontBody = Inter({
  subsets: ["latin", "cyrillic"],
  variable: "--font-body",
  display: "swap",
});

export const fontDisplay = Fraunces({
  subsets: ["latin", "cyrillic"],
  variable: "--font-display",
  display: "swap",
});
```

```tsx
// src/app/layout.tsx
import { fontBody, fontDisplay } from "./fonts";

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={`${fontBody.variable} ${fontDisplay.variable}`}>
      <body className="font-body bg-background text-foreground">{children}</body>
    </html>
  );
}
```

**Tailwind mapping (example)**

```ts
// tailwind.config.ts (extend)
export default {
  theme: {
    extend: {
      fontFamily: {
        body: ["var(--font-body)"],
        display: ["var(--font-display)"],
      },
      fontSize: {
        h1: ["var(--text-h1)", { lineHeight: "var(--leading-h1)", letterSpacing: "var(--tracking-h1)" }],
        h2: ["var(--text-h2)", { lineHeight: "var(--leading-h2)", letterSpacing: "var(--tracking-h2)" }],
        h3: ["var(--text-h3)", { lineHeight: "var(--leading-h3)", letterSpacing: "var(--tracking-h3)" }],
        body: ["var(--text-body)", { lineHeight: "var(--leading-body)", letterSpacing: "var(--tracking-body)" }],
        sm: ["var(--text-sm)", { lineHeight: "var(--leading-sm)", letterSpacing: "var(--tracking-sm)" }],
      },
    },
  },
};
```

**Text scale rules of thumb**

- Keep **4–6 sizes total**; declare once and reuse (no ad-hoc sizes per component).
- Prefer consistent line-height:
  - headings: ~1.1–1.2
  - body: ~1.5–1.7
- If you need a new size, add it to the scale (don’t “just this once” in a component).

---

## 4) Palette

### 4.1 Baseline structure

- **Neutrals:** background / surfaces / borders / muted text
- **One accent:** primary/accent + foreground
- **Destructive:** error states

### 4.2 Rules

- Build palettes for **states** (hover/focus/disabled), not just static screenshots.
- Avoid low-contrast “gray on gray” text.
- Use tokens; do not sprinkle arbitrary hex values across components.

---

## 5) Tokens

### 5.1 Semantic color token set (shadcn-compatible)

Prefer a shadcn-compatible semantic set:

- `--background`, `--foreground`
- `--card`, `--card-foreground`
- `--popover`, `--popover-foreground`
- `--primary`, `--primary-foreground`
- `--secondary`, `--secondary-foreground`
- `--muted`, `--muted-foreground`
- `--accent`, `--accent-foreground`
- `--destructive`, `--destructive-foreground`
- `--border`, `--input`, `--ring`

Optional product state tokens (add only when needed):

- `--success`, `--success-foreground`
- `--warning`, `--warning-foreground`
- `--info`, `--info-foreground`

### 5.2 Non-color tokens (minimum baseline)

Also define:

- `--radius` (base)
- elevation/shadow tokens: `--shadow-sm`, `--shadow-md` (minimum 2 levels)
- motion tokens: `--motion-fast`, `--motion-normal`, `--motion-slow`
- `--ease-out` (single primary easing)

### 5.3 State + interaction conventions

- Hover/active should be consistent:
  - Prefer opacity variants (e.g., `hover:bg-primary/90`, `active:bg-primary/85`) over new hex values.
  - If you need app-wide “tint” behavior, add derived tokens (e.g., `--primary-hover`)
    computed via `color-mix()` and map them to Tailwind.
- Disabled state:
  - Prefer opacity + pointer-events (e.g., `disabled:opacity-50 disabled:pointer-events-none`).
- Never add “one-off” colors in components. If a new semantic is required, add a token.

### 5.4 Implementation contract (copy/paste baseline)

**Contract:** tokens live in CSS variables (single source of truth). Tailwind maps to those variables.
Components use semantic utilities (e.g., `bg-background`, `text-foreground`, `bg-primary`).

**`src/app/globals.css` (example)**

```css
:root {
  --background: 0 0% 100%;
  --foreground: 222.2 84% 4.9%;
  --card: 0 0% 100%;
  --card-foreground: 222.2 84% 4.9%;
  --primary: 222.2 47.4% 11.2%;
  --primary-foreground: 210 40% 98%;
  --border: 214.3 31.8% 91.4%;
  --ring: 222.2 84% 4.9%;

  --shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.06), 0 1px 1px -1px rgb(0 0 0 / 0.06);
  --shadow-md: 0 10px 15px -3px rgb(0 0 0 / 0.12), 0 4px 6px -4px rgb(0 0 0 / 0.12);

  --radius: 0.75rem;

  --motion-fast: 120ms;
  --motion-normal: 180ms;
  --motion-slow: 260ms;
  --ease-out: cubic-bezier(0.16, 1, 0.3, 1);
}

.dark {
  --background: 222.2 84% 4.9%;
  --foreground: 210 40% 98%;
  --card: 222.2 84% 4.9%;
  --card-foreground: 210 40% 98%;
  --primary: 210 40% 98%;
  --primary-foreground: 222.2 47.4% 11.2%;
  --border: 217.2 32.6% 17.5%;
  --ring: 212.7 26.8% 83.9%;
}
```

**Tailwind mapping (example)**

```ts
// tailwind.config.ts (extend)
export default {
  theme: {
    extend: {
      colors: {
        border: "hsl(var(--border))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
      },
      boxShadow: {
        sm: "var(--shadow-sm)",
        md: "var(--shadow-md)",
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      transitionTimingFunction: {
        "ease-out": "var(--ease-out)",
      },
      transitionDuration: {
        fast: "var(--motion-fast)",
        normal: "var(--motion-normal)",
        slow: "var(--motion-slow)",
      },
    },
  },
};
```

**Component usage (example)**

```tsx
<button className="rounded-lg bg-primary text-primary-foreground shadow-sm transition-[transform,opacity] duration-normal ease-ease-out hover:-translate-y-0.5 hover:bg-primary/90 active:bg-primary/85">
  Continue
</button>
```

### 5.5 Focus-visible pattern (copy/paste)

Make focus styles **consistent and visible** across interactive primitives:

```txt
focus-visible:outline-none
focus-visible:ring-2 focus-visible:ring-ring
focus-visible:ring-offset-2 focus-visible:ring-offset-background
```

Use it directly or via shared component variants. Do not ship “invisible focus”.

---

## 6) Style recipes (direction rails)

Recipes are not templates. They are constraints that help you pick coherent defaults quickly.

### 6.1 Editorial Tech (dark)

- Dark neutral base with subtle texture and crisp borders.
- One cool accent used sparingly.
- Strong display type; calm, readable body type.
- One signature interaction (e.g., staggered hero reveal).

### 6.2 Clean Studio (light)

- Bright surfaces, thin shadows, strict whitespace discipline.
- One clean accent (blue/green/red), no gradient clichés.
- Hover micro-interactions (lift, underline, icon shift) kept subtle.

### 6.3 Industrial Utility (enterprise)

- Grid-driven layout, strict hierarchy, readable density.
- Neutral palette + one accent.
- Minimal decoration; maximum clarity and predictability.

---

## 7) Layout primitives (avoid wrapper-only nesting)

Use a small set of primitives consistently:

- **Container:** max width + horizontal padding
- **Section:** vertical rhythm (top/bottom spacing)
- **Stack:** vertical layout using `gap`
- **Cluster:** horizontal groups using `gap` + wrap
- **Grid:** responsive columns (avoid per-card hacks)

Rules:

- Spacing *between* blocks → `gap` on the parent (Stack/Grid).
- Padding *inside* cards → one place (don’t “sprinkle padding” on every nested layer).
- Prefer 2–4 nesting levels; deeply nested wrappers must justify themselves.

**Copy/paste Tailwind class recipes (baseline)**

```txt
Container: mx-auto w-full max-w-6xl px-4 md:px-6 lg:px-8
Section: py-12 md:py-16
Stack: flex flex-col gap-4
Cluster: flex flex-wrap items-center gap-3
Grid (2-col): grid grid-cols-1 gap-6 md:grid-cols-2
Grid (3-col): grid grid-cols-1 gap-6 md:grid-cols-3
```

Adjust `px-*`, `py-*`, and `gap-*` using the spacing scale in §7.1. Avoid ad-hoc values.

### 7.1 Baseline: container widths + spacing scale

**Container baseline (default)**

- Max width: **72rem (1152px)** for marketing pages and general UI.
- Side padding: `px-4` on mobile; `md:px-6` or `lg:px-8` on larger screens.
- For long-form text, cap reading width around **65ch**.

**Spacing scale (px → Tailwind)**

- 4 → `1`
- 8 → `2`
- 12 → `3`
- 16 → `4`
- 24 → `6`
- 32 → `8`
- 48 → `12`

**Recommended defaults**

- Card padding: `p-4` (16px) or `p-6` (24px)
- Stack gaps: `gap-3` (12px) to `gap-6` (24px)
- Section spacing: `py-12 md:py-16` (48–64px)
- Hero spacing (when needed): `py-16 md:py-20` (64–80px)

### 7.2 Fix spacing/alignment quickly (debug protocol)

When something looks “off”:

1) Remove wrapper-only nodes first (if it adds no layout/semantics, it is noise).
2) Re-establish a single spacing source of truth:
   - between blocks → `gap`
   - inside cards → one padding layer
3) Temporarily enable debug styling (dev-only):
   - `outline: 1px solid ...` or `ring-1`
   - highlight containers vs content
4) Only then adjust cosmetics (shadows, gradients, borders).

---

## 8) Component baseline (minimum)

Even before a full UI kit exists, keep these stable:

- Button (variants + sizes)
- Input / Textarea / Select
- Card (at least 2 elevation levels)
- Badge/Tag
- Tabs
- Dialog/Drawer
- Tooltip
- Toast/Notification
- Data table (when required)

If using shadcn/ui, prefer generating components from it and customizing via tokens and variants.

---

## 9) Motion (smooth, deliberate)

- Prefer `transform` + `opacity` for 60fps.
- Use **1–2 signature moments** per page (hero entry, interactive blocks).
- Default to subtle motion. If it draws attention, it must earn it.
- Always respect `prefers-reduced-motion` (disable non-essential motion).

### 9.1 Implementation pattern (Tailwind)

Gate “nice-to-have” animation behind `motion-safe:` and provide `motion-reduce:` fallbacks:

```tsx
<button
  className="
    transition duration-normal ease-ease-out
    motion-safe:hover:-translate-y-0.5 motion-safe:hover:shadow-md
    motion-reduce:transform-none motion-reduce:shadow-none
    motion-reduce:transition-none
  "
>
  Continue
</button>
```

- Use `motion-safe:` for entry transitions, hover transforms, and parallax-like effects.
- In reduced motion, keep UI responsive: remove transforms and long transitions, but keep clarity.

---

## 10) UI QA checklist

### Visual clarity

- Hierarchy is obvious (headings, subheadings, body).
- Body text is readable: comfortable line-height and no low-contrast gray-on-gray.

### Spacing consistency

- Similar components have identical paddings and gaps.
- Layout aligns to a consistent container and spacing scale.

### Interaction states

- Hover/focus/active/disabled states are defined where applicable.
- Keyboard navigation works for interactive elements.

### Accessibility baseline (practical, numeric)

- Color contrast meets **WCAG AA** for text (or better).
- Focus ring is visible: **≥ 2px** thickness with an offset.
- Minimum interactive hit target: **44×44px** for touch targets.
- `prefers-reduced-motion`: disable non-essential animations and remove large parallax effects.

### Responsive

- No broken layout on mobile.
- Density is intentional across 2–3 breakpoints (not “shrunk desktop”).

### Performance

- Avoid heavy, large-area blur/glow layers.
- Avoid animating layout properties (`width`, `height`, `top`, etc.) when possible.

---

## 11) Prompt formula (how to ask Codex for UI work)

Use a short, structured request:

1) Propose 2 style directions (name + 5 bullets each).
2) Pick 1 direction and update `docs/STYLE_GUIDE.md` (typography + palette + tokens).
3) Implement in small checkpoints (primitives → components → polish).
4) End with diff + checklist of manual UI verifications.
