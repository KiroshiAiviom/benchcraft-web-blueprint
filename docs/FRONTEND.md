# Frontend

Baseline frontend conventions for **Next.js (App Router)** projects using this blueprint.

This document is not a full style guide.
It defines a few **defaults** that keep the repo consistent and easy for agents to work in.

## Directory conventions (suggested)

- `app/` — routes, layouts, route-level UI
- `components/` — reusable UI primitives and compositions
- `lib/` — helpers (server/client separated where needed)
- `styles/` — globals (if any)

If the project already has a structure, keep it — just document it in this file.

## Data fetching & side effects (baseline)

- Prefer server-side data fetching (Route Handlers / Server Actions / server components) where it improves security and simplicity.
- Treat client-side fetching as a deliberate choice (latency/UX), not a default.
- Keep side effects (writes) server-authoritative.

## UI implementation contracts

### Token-only styling discipline

- Repeated values must come from documented tokens (spacing, color, typography, radius, shadow, motion).
- Avoid one-off raw values for spacing/colors in component/page code unless explicitly approved.
- Prefer semantic styling hooks over ad-hoc values (for example: tokenized classes/CSS vars).

### Icon consistency contract

- Default icon library: Lucide (`lucide-react`) if icons are needed.
- Keep one icon family per project/page set unless explicitly approved otherwise.
- Standardize size/stroke per context (for example: nav, action buttons, dense data rows).
- Do not mix icon weights/styles in the same UI context.

### Focus-visible (Tailwind)

Use a visible focus ring by default:

```txt
focus-visible:outline-none
focus-visible:ring-2 focus-visible:ring-ring
focus-visible:ring-offset-2 focus-visible:ring-offset-background
```

### Hit targets

- Icon buttons: `min-h-11 min-w-11 p-2`
- Dense rows/toolbars: keep `min-h-11`; reduce spacing *around* controls, not the target.

### Motion gating

- Gate non-essential motion with `motion-safe:*`.
- Provide `motion-reduce:*` fallbacks (trim transitions; remove transforms/parallax).

### Elevation token usage

- Use documented elevation tokens only; no ad-hoc shadow strings in page/component code.
- Keep elevation tiers shallow (for example: base, raised, overlay) unless a design-system decision says otherwise.
- Depth should support hierarchy, not decorate everything.

### Spacing and layout flow

- Prefer `gap-*` for stack/grid spacing over manual sibling margins.
- Keep spacing decisions in layout primitives and component internals, not scattered in pages.
- Avoid margin-collapsing-dependent layout behavior.

### Density modes and spacing ramps

- Use explicit density modes (comfortable/compact) backed by tokens.
- Compact mode reduces whitespace around content, not usability targets.
- Keep touch target baseline intact even in compact layouts.

### Content width and readability defaults

- Long-form content surfaces should use readable line lengths (~45-75 chars).
- Dense application surfaces can be compact, but preserve clear grouping and scanability.
- Prefer max-width-constrained content containers for text-heavy screens.

## Component patterns

- Prefer a small set of layout primitives (Container / Section / Stack / Grid).
- Avoid wrapper-only nesting; add a wrapper only if it carries semantics or behavior.
- Keep components “boring”: predictable props, minimal implicit behavior.
- Build pages from primitives/composed components first; avoid page-level bespoke spacing systems.
- For interactive components/surfaces, cover states where applicable:
  - hover / focus-visible / active / disabled / loading / empty / error

## Quality gates (frontend)

- Lint + typecheck on every meaningful code checkpoint.
- Manual UI QA for UI changes (see `docs/DESIGN.md`).
- Manual UI QA should include required viewports and quick evidence notes in the checkpoint report.
- If visual regression tooling exists in the project, run it for user-facing UI changes.

## References

- Design/UX guardrails: `docs/DESIGN.md`
- Quality rubric: `docs/QUALITY_SCORE.md`
- UI detail canon: `docs/references/ui-taste-playbook-llms.txt`
