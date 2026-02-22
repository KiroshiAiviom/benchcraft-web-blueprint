# Design System — <Project Name>

> This is the **single source of truth** for UI decisions (typography, palette, tokens, layout primitives, components, motion).
> The build agent must **not** invent new colors/spacing/shadows outside this file.

---

## 1) UI direction (high-level)

- Aesthetic: <calm / premium / compact / professional>
- Visual goals (choose 3–5):
  - <Text clarity>
  - <Clean hierarchy>
  - <Crisp spacing>
  - <Tasteful micro-interactions>
- Anti-goals (avoid):
  - “AI-template” aesthetics, overused fonts, random gradients
  - Inconsistent spacing and misaligned baselines
  - Excessive wrappers / div soup

## 2) Typography (typography-first)

### 2.1 Font shortlist

- Body: <font>
- Display/heading: <font>
- Mono (optional): <font>

### 2.2 Font source standard

- Default source: Google Fonts via `next/font/google`.
- Use local fonts (`next/font/local`) only when project constraints require it.
- Document font source decisions and licensing constraints in this file.

### 2.3 Type scale

Define a **small, enforceable** scale:

| Token | Example use |
|---|---|
| `--text-h1` | hero headline |
| `--text-h2` | section headline |
| `--text-h3` | card headline |
| `--text-body` | normal body text |
| `--text-sm` | helper / meta |

Add line-height + letter-spacing tokens if needed.

## 3) Color palette

### 3.1 Palette roles

- Background
- Surface
- Foreground
- Primary
- Secondary
- Muted
- Border
- Destructive
- (Optional) Success / Warning / Info

### 3.2 Rules

- Prefer semantic tokens (e.g. `--primary`) over hardcoded hex values.
- Colors must support light + dark themes.
- Keep it restrained: 1 primary + 1 secondary + neutrals.

## 4) Design tokens

> Tokens are the enforcement layer. If a value repeats, it becomes a token.

### 4.1 Required semantic tokens

- Colors:
  - `--background`, `--foreground`, `--surface`, `--surface-2`
  - `--primary`, `--primary-foreground`
  - `--secondary`, `--secondary-foreground`
  - `--muted`, `--muted-foreground`
  - `--border`
  - `--destructive`, `--destructive-foreground`
  - (Optional) `--success`, `--warning`, `--info`
- Radius:
  - `--radius-sm`, `--radius-md`, `--radius-lg`
- Elevation:
  - `--shadow-sm`, `--shadow-md` (add `--shadow-lg` only if truly needed)
  - `--elevation-surface`, `--elevation-raised`, `--elevation-overlay` (tokenized layer usage)
- Density:
  - `--density-comfortable`, `--density-compact`
- Motion:
  - `--ease-standard`, `--duration-fast`, `--duration-base`
- Typography:
  - `--font-body`, `--font-display`
  - `--text-*` scale
- Fine detail:
  - `--divider-subtle`, `--border-subtle`, `--focus-ring`, `--focus-ring-offset`

### 4.2 Interaction/state conventions

Define how hover/active/disabled are derived:

- Prefer tokenized variants (`--primary-hover`, `--primary-active`) **or** a documented derivation (e.g., `color-mix()`), but do not mix ad-hoc approaches.
- Focus ring must be consistent across components.
- Divider/border subtlety should be tokenized, not improvised per component.

### 4.3 Detail token guidance

- Elevation layers:
  - define where `surface`, `raised`, and `overlay` layers are used.
  - pair elevation with border contrast when needed for clear depth.
- Density tokens:
  - define compact vs comfortable spacing behavior per major surface type.
- Fine-stroke details:
  - use tokenized subtle borders/dividers for structure without visual clutter.
- Focus styling:
  - use tokenized ring color and offset for consistent focus affordance.

### 4.4 Implementation contract (copy/paste baseline)

> This contract makes tokens real: CSS variables → Tailwind mapping → component usage.

> **Important:** do not blindly copy/paste typography choices from a template.
> First, decide fonts in **§2 Typography**, then wire them here.

`src/app/globals.css` (example skeleton):

```css
:root {
  /* Typography */
  /* Provided by next/font via CSS variables on <html>. */
  /* --font-body: <set via next/font> */
  /* --font-display: <set via next/font> */

  /* Type scale (examples) */
  --text-h1: 2.25rem;
  --text-h2: 1.875rem;
  --text-h3: 1.5rem;
  --text-body: 1rem;
  --text-sm: 0.875rem;

  /* Colors */
  --background: 0 0% 100%;
  --foreground: 222.2 84% 4.9%;
  --primary: 222.2 47.4% 11.2%;
  --primary-foreground: 210 40% 98%;
  --border: 214.3 31.8% 91.4%;

  /* Radius + elevation */
  --radius-md: 12px;
  --shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.06);
  --shadow-md: 0 8px 24px -12px rgb(0 0 0 / 0.24);

  /* Motion */
  --duration-fast: 120ms;
  --duration-base: 180ms;
  --ease-standard: cubic-bezier(0.2, 0, 0, 1);
}

.dark {
  --background: 222.2 84% 4.9%;
  --foreground: 210 40% 98%;
  --primary: 210 40% 98%;
  --primary-foreground: 222.2 47.4% 11.2%;
  --border: 217.2 32.6% 17.5%;
}
```

`tailwind.config.ts` (token wiring pattern):

```ts
import type { Config } from "tailwindcss";

const config: Config = {
  theme: {
    extend: {
      colors: {
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        border: "hsl(var(--border))",
      },
      borderRadius: {
        md: "var(--radius-md)",
      },
      boxShadow: {
        sm: "var(--shadow-sm)",
        md: "var(--shadow-md)",
      },
      transitionTimingFunction: {
        standard: "var(--ease-standard)",
      },
      transitionDuration: {
        fast: "var(--duration-fast)",
        base: "var(--duration-base)",
      },
    },
  },
};

export default config;
```

`src/app/layout.tsx` (Next.js font wiring pattern):

```tsx
// Choose your fonts in §2 Typography. Replace the placeholders below.
import { <BodyFont>, <DisplayFont> } from "next/font/google";

const body = <BodyFont>({ subsets: ["latin"], variable: "--font-body" });
const display = <DisplayFont>({ subsets: ["latin"], variable: "--font-display" });

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={`${body.variable} ${display.variable}`}>
      <body className="font-[var(--font-body)] bg-background text-foreground">
        {children}
      </body>
    </html>
  );
}
```

## 5) Layout primitives (mandatory)

> Use these to avoid wrapper-only nesting and inconsistent spacing.

### 5.1 Spacing scale

- Base spacing scale (example): `4 / 8 / 12 / 16 / 24 / 32 / 48 / 64`
- Prefer `gap-*` over manual margins for stacks/grids.

### 5.2 Class recipes (copy/paste)

```txt
Container  : mx-auto w-full max-w-6xl px-4 sm:px-6 lg:px-8
Section    : py-12 sm:py-16 lg:py-20
Stack (v)  : flex flex-col gap-4
Stack (h)  : flex flex-row items-center gap-3
Grid (2/3) : grid gap-6 sm:grid-cols-2 lg:grid-cols-3
Card base  : rounded-md border bg-background shadow-sm
```

## 6) Components (inventory + rules)

### 6.1 Component baseline

- Build and maintain project components in-house, aligned to this Design System.
- Prefer composition over deep wrapper nesting.
- Every interactive component must cover:
  - hover / focus-visible / active
  - disabled (when applicable)
  - loading (when applicable)
  - empty + error states for data surfaces

### 6.2 Required core components

- Button (primary / secondary / ghost)
- Input / Textarea / Select
- Card (at least 2 elevation levels)
- Badge
- Tooltip
- Dialog / Sheet
- Toast / inline error message

### 6.3 Iconography standard

- Default icon library: `lucide-react`.
- Keep one icon family per project unless explicitly approved otherwise.
- Define size/stroke usage by context (for example: nav, buttons, data rows).
- Do not mix icon families/styles without explicit approval.

## 7) Motion (polish, not noise)

- Default transitions:
  - use `--duration-*` and `--ease-standard`
  - keep durations short (120–220ms)
- Use Tailwind’s motion utilities:
  - gate non-essential motion with `motion-safe:*`
  - disable/trim motion with `motion-reduce:*`

Example pattern:

```tsx
<button
  className="transition-transform duration-base ease-standard motion-safe:hover:scale-[1.02] motion-reduce:transform-none"
>
  …
</button>
```

## 8) Accessibility baseline

- Contrast: target WCAG AA for text.
- Focus ring: **≥ 2px** with visible offset.
- Hit targets: **≥ 44×44px** for touch.
- Keyboard navigation must work for all interactive elements.

Focus-visible example:

```tsx
<button className="focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-primary focus-visible:ring-offset-2">
  …
</button>
```

## 9) Screen-level UI notes (optional)

> If your project has multiple screens, capture the UI intent here so the build agent doesn’t guess.

- `/route`:
  - Primary goal:
  - Key components:
  - States (loading/empty/error):
  - Responsive notes:
  - Variant reference (required for key routes): `<variant-file>#<variant-id>`

## 10) QA checklist

- [ ] Typography scale is consistent (no random `text-*` choices).
- [ ] Tokens are used (no hardcoded colors/shadows for repeated values).
- [ ] Layout primitives used (no wrapper soup).
- [ ] Focus and keyboard navigation verified.
- [ ] `prefers-reduced-motion` respected.
