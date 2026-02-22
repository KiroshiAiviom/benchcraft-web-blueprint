# Design

A compact set of design/UX guardrails for agent-driven UI work.

- Project-specific tokens and component rules belong in `docs/DESIGN_SYSTEM.md`.
- Implementation details belong in `docs/FRONTEND.md`.
- Micro-detail canon and scoring live in `docs/references/ui-taste-playbook-llms.txt`.

## When to read

Use this for any checkpoint that touches:

- layout / spacing / typography
- styling / theming
- components / iconography
- motion / interactions
- UX polish

## Taste invariants (mandatory)

- Typography-first:
  - readable text hierarchy with stable type scale.
  - body copy target line length: ~45-75 characters.
- Token discipline:
  - repeated values become tokens in `docs/DESIGN_SYSTEM.md`.
  - no one-off repeated hex/spacing/shadow values.
- Spacing rhythm and density:
  - use consistent spacing scale + `gap`-first flow.
  - minimum spacing rhythm must stay consistent across comparable surfaces.
  - compact mode is allowed only via explicit density tokens, not ad-hoc shrinking.
- Hierarchy and contrast:
  - primary action and primary content must be obvious fast.
  - use emphasis/de-emphasis intentionally.
- Icon consistency:
  - single icon family per project/page set (default: Lucide).
  - consistent icon size/stroke strategy per context.
- Depth/elevation:
  - depth is one detail among many.
  - use tokenized elevation tiers; avoid random shadow mixes.
- Accessibility baseline:
  - visible focus ring, keyboard navigation, sensible contrast, touch target sanity.
- Motion is deliberate:
  - respect `prefers-reduced-motion`; no decorative motion noise.
- Content scanability:
  - concise, specific labels and copy.
  - empty/error states must instruct next action.

## Variant-first checkpoint gate (required for key page UI)

Before implementing key page UI:
1) Produce 5 page variants (3 for low-risk pages) using docs-first outlines.
2) Store variants in `docs/templates/UI_PAGE_VARIANTS_TEMPLATE.md` shape.
3) Score variants using the rubric in `docs/references/ui-taste-playbook-llms.txt`.
4) Stop for human-selected variant ID.

No page UI implementation starts before selection is confirmed in thread.

## UI feedback loop (required for UI checkpoints)

1) Variant exploration + selection gate (where applicable).
2) Implement with tokens + layout primitives.
3) Render and review at required viewports.
4) Run UI audit (manual today; visual diffs when available).
5) Patch inconsistencies before checkpoint handoff.

## UI audit contract

Every UI checkpoint should include a short audit summary in the report:

- Spacing + density:
  - list spacing values used and confirm mapping to spacing scale/tokens.
  - confirm chosen density mode and any exceptions.
- Typography:
  - list type tokens/styles used and confirm consistent hierarchy/line length.
- Hierarchy + contrast:
  - confirm primary action clarity and readable contrast in context.
- Iconography:
  - confirm single family usage and consistent sizing/stroke approach.
- States:
  - confirm hover/focus/active/disabled/loading/empty/error where applicable.
- Accessibility quick checks:
  - focus-visible, keyboard traversal, contrast sanity.
- Responsive sanity:
  - note desktop + mobile checks and intentional exceptions.

## Anti-patterns

Avoid by default:

- generic hero + cards with no product-specific hierarchy decisions
- random glow/blur/depth effects as polish substitute
- deep wrapper-only DOM nesting
- random spacing or color tweaks scattered across pages
- mixed icon families in the same product surface
- copying aesthetics without explicit design decisions

## Operating modes

- Audit-only: when scope is unclear ("make it better"). Produce phased plan and stop.
- Build: implement approved scope in small checkpoints.

(Protocol: `.codex/skills/role-ui`.)

## QA baseline

- Viewports: 375x812, 768x1024, 1024x768, 1440x900
- Keyboard: tab through controls; focus always visible
- Reduced motion: verify with `prefers-reduced-motion`
- Evidence: include before/after screenshots for UI-impacting checkpoints when practical

## How to request UI work (prompt formula)

1) Context: screen/flow + user problem.
2) Constraints: tokens, no new deps, mobile-first, etc.
3) Ask for either:
   - Audit-only (plan + recommendations), or
   - Build (next small approved step).
