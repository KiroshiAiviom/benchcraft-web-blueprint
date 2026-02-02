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
  - H1 / H2 / H3 / body / small
  - line-height and letter-spacing included
- Prefer variable fonts where possible.
- Ensure language coverage (Cyrillic/extended Latin/etc.) before committing.

### 3.2 Quick shortlist (display + body pairs)

These are “good defaults” that avoid common AI-generated aesthetics. Use them as a starting point.

- IBM Plex Sans (body) + IBM Plex Serif (display)
- Source Sans 3 (body) + Source Serif 4 (display)
- Fira Sans (body) + Alegreya (display)
- PT Sans (body) + PT Serif (display) — strong Cyrillic support
- Noto Sans (body) + Noto Serif (display) — broad language support
- Manrope (body) + Spectral (display)

---

## 4) Palette

### 4.1 Baseline structure

- **Neutrals:** background / surfaces / borders / muted text
- **One accent:** accent + accent-foreground
- Optional: **danger** (error states)

### 4.2 Rules

- Build palettes for **states** (hover/focus/disabled), not just static screenshots.
- Avoid low-contrast “gray on gray” text.
- Use tokens; do not sprinkle arbitrary hex values across components.

---

## 5) Tokens

### 5.1 Minimal token set (semantic)

Colors (minimum):

- `--background`, `--foreground`
- `--card`, `--card-foreground`
- `--muted`, `--muted-foreground`
- `--border`, `--input`
- `--accent`, `--accent-foreground`
- `--ring` (focus)

Shape:

- `--radius` (base)

Motion:

- `--motion-fast`, `--motion-normal`, `--motion-slow`
- `--ease-out` (single primary easing)

### 5.2 Implementation contract (copy/paste baseline)

**Contract:** tokens live in CSS variables (single source of truth). Tailwind maps to those variables.
Components use Tailwind semantic classes (e.g., `bg-background`, `text-foreground`).

**`app/globals.css` (or `src/app/globals.css`)**
```css
:root {
  /* colors (HSL components; compatible with shadcn/ui conventions) */
  --background: 0 0% 100%;
  --foreground: 240 10% 3.9%;
  --card: 0 0% 100%;
  --card-foreground: 240 10% 3.9%;
  --muted: 240 4.8% 95.9%;
  --muted-foreground: 240 3.8% 46.1%;
  --border: 240 5.9% 90%;
  --input: 240 5.9% 90%;
  --accent: 240 4.8% 95.9%;
  --accent-foreground: 240 5.9% 10%;
  --ring: 240 5% 64.9%;

  /* shape */
  --radius: 0.75rem;

  /* motion */
  --motion-fast: 120ms;
  --motion-normal: 180ms;
  --motion-slow: 260ms;
  --ease-out: cubic-bezier(0.16, 1, 0.3, 1);
}

.dark {
  --background: 240 10% 3.9%;
  --foreground: 0 0% 98%;
  --card: 240 10% 3.9%;
  --card-foreground: 0 0% 98%;
  --muted: 240 3.7% 15.9%;
  --muted-foreground: 240 5% 64.9%;
  --border: 240 3.7% 15.9%;
  --input: 240 3.7% 15.9%;
  --accent: 240 3.7% 15.9%;
  --accent-foreground: 0 0% 98%;
  --ring: 240 4.9% 83.9%;
}
```

**`tailwind.config.ts` (extend mapping)**
```ts
export default {
  theme: {
    extend: {
      colors: {
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        card: "hsl(var(--card))",
        "card-foreground": "hsl(var(--card-foreground))",
        muted: "hsl(var(--muted))",
        "muted-foreground": "hsl(var(--muted-foreground))",
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        accent: "hsl(var(--accent))",
        "accent-foreground": "hsl(var(--accent-foreground))",
        ring: "hsl(var(--ring))",
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
<button className="rounded-lg bg-accent text-accent-foreground transition-[transform,opacity] duration-normal ease-ease-out hover:-translate-y-0.5">
  Continue
</button>
```

---

## 6) Style recipes (direction rails)

Recipes are not templates. They are constraints that help you pick coherent defaults quickly.

### 6.1 Editorial Tech (dark)

- Dark neutral base with subtle texture and crisp borders.
- One cool accent used sparingly.
- Strong display type; calm, readable body type.
- One “signature” interaction (e.g., staggered hero reveal).

### 6.2 Clean Studio (light)

- Bright surfaces, thin shadows, strong whitespace discipline.
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

### 7.1 Fix spacing/alignment quickly (debug protocol)

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
- Use **1–2 signature moments** per page:
  - hero entry stagger
  - a small set of interactive blocks
- Always respect `prefers-reduced-motion` (disable non-essential motion).

---

## 10) UI QA checklist

### Visual clarity

- Hierarchy is obvious (headings, subheadings, body).
- Body text is readable: comfortable line-height and no low-contrast gray-on-gray.

### Spacing consistency

- Similar components have identical paddings and gaps.
- Layout aligns to a consistent grid/container.

### Interaction states

- Hover/focus/active/disabled states are defined where applicable.
- Keyboard navigation works for interactive elements.

### Accessibility baseline (practical, numeric)

- Color contrast meets **WCAG AA** for text (or better).
- Focus ring is visible: **≥ 2px** thickness with an offset (avoid “inset-only” focus).
- Minimum interactive hit target: **44×44px** for touch targets.
- `prefers-reduced-motion`: disable non-essential animations and remove large parallax effects.

### Responsive

- No broken layout on mobile.
- Density is intentional across 2–3 breakpoints (not “shrunk desktop”).

### Performance

- Avoid heavy, large-area blur/glow layers.
- No janky animation: avoid animating layout properties (`width`, `height`, `top`, etc.) when possible.

---

## 11) Prompt formula (how to ask Codex for UI work)

Use a short, structured request:

1) Propose 2 style directions (name + 5 bullets each).
2) Pick 1 direction and write/update `docs/STYLE_GUIDE.md` tokens + typography.
3) Implement the UI in small checkpoints.
4) End with diff + checklist of manual UI verifications.

