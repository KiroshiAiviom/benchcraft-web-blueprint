# UI Detail Principles (Blueprint Notes)

This file captures implementation-ready UI detail practices for this blueprint.
Use it as the detailed companion to `docs/references/ui-taste-playbook-llms.txt`.

## 1) Workflow and sequencing

- Start from a concrete feature flow, not global shell styling.
- Sketch multiple layout directions before visual polish.
- Resolve hierarchy and spacing before introducing strong color.
- Work in short cycles: outline -> build -> test with real content -> refine.

## 2) Hierarchy and emphasis

- Each screen section should have one dominant action or focal point.
- Differentiate priorities using a combination of:
  - size
  - contrast
  - position
  - whitespace
  - weight
- De-emphasize secondary info instead of over-emphasizing everything.
- Keep heading hierarchy visual, not tied rigidly to HTML heading size defaults.

Quick checks:
- 5-second scan: can a new user identify primary action and key content blocks?
- Squint test: are major blocks and action hierarchy still obvious?

## 3) Spacing rhythm and density

- Define a spacing scale and stick to it.
- Prefer gap-based layouts over ad-hoc sibling margins.
- Use larger spacing between groups and smaller spacing within groups.
- Avoid ambiguous spacing where relationships are visually unclear.

Density rules:
- Comfortable mode: default for marketing/content pages.
- Compact mode: data-dense product surfaces only.
- Compact must not reduce control hit targets or destroy readability.

Quick checks:
- List unique spacing values in the screen: all should map to tokens.
- Group boundaries should be visually clearer than within-group spacing.

## 4) Typography and readability

- Use a small, explicit type scale.
- Keep body line length around 45-75 characters.
- Increase line-height as text gets smaller or line length gets longer.
- Use letter spacing intentionally:
  - tighter for large display text
  - slightly looser for uppercase micro-labels
- Align text blocks for readability first, not decorative centering.

Quick checks:
- Dense paragraphs remain readable on both desktop and mobile.
- Micro-labels and metadata remain legible without zoom.

## 5) Color and contrast systems

- Use semantic color roles, not ad-hoc palette picks.
- Build neutral ramps strong enough for backgrounds, surfaces, and dividers.
- Define shade ramps before component-level polish.
- Do not rely on color alone for meaning (pair with text/icon/shape/state).

Quick checks:
- Primary and secondary actions are distinguishable in all supported themes.
- Critical text remains readable on tinted/colored backgrounds.

## 6) Depth, borders, and surface layering

- Use depth to communicate structure, not decoration.
- Keep a small set of elevation tiers (for example: base, raised, overlay).
- Pair subtle borders with shadows where needed for edge clarity.
- Use consistent light direction assumptions across shadows/highlights.

Quick checks:
- Elevated surfaces feel intentionally layered, not randomly floating.
- Flat surfaces still read as structured through spacing and contrast.

## 7) Motion and interaction feedback

- Motion should clarify state and orientation.
- Keep transitions short and consistent.
- Respect `prefers-reduced-motion`.
- Use micro-interactions on high-value moments only (focus change, expand/collapse, submit feedback).

Quick checks:
- Motion never blocks task completion.
- Reduced-motion users get equivalent clarity without transform-heavy effects.

## 8) Iconography and visual language

- Use one icon family per product surface.
- Keep icon size/stroke/optical weight consistent per context.
- Do not use icons as decoration when they add no semantic value.
- Pair ambiguous icons with labels.

Quick checks:
- Icons in one row/toolbar feel like the same language set.
- Removing icons from a screen should not destroy comprehensibility.

## 9) Element-level quality patterns

### 9.1 Buttons and CTAs

- Primary button must be visually distinct from secondary/ghost actions.
- Keep button text specific to action intent.
- Ensure hover/focus/active/disabled/loading states are all present.
- Avoid multiple primary CTAs competing within the same local group.

### 9.2 Inputs and forms

- Labels should be visible and clear (placeholder is not label replacement).
- Group related fields; use helper text only when needed.
- Show validation states near the field and explain recovery action.
- Keep form alignment and spacing rhythm consistent.

### 9.3 Tables and data grids

- Prioritize scanability: clear column hierarchy and row rhythm.
- Avoid heavy borders everywhere; use subtle separators + spacing.
- Keep numeric data alignment consistent (usually right-aligned for comparable numeric columns).
- Preserve sticky headers/actions where context loss is likely.

### 9.4 Cards and panels

- Cards should communicate grouping, not arbitrary decoration.
- Use consistent internal spacing and heading structure.
- Elevation differences should reflect interaction/importance differences.

### 9.5 Navigation systems

- Current location must be obvious.
- Avoid equal visual weight across all nav options.
- Keep nav rhythm and icon/text pairing consistent.
- Support keyboard focus visibility in all nav patterns.

### 9.6 Dialogs, drawers, overlays

- Make context, consequence, and primary action explicit.
- Keep destructive actions visually and spatially separated.
- Ensure backdrop + elevation make layering obvious.

### 9.7 Empty, loading, and error states

- Empty state explains what the surface is for and what to do next.
- Loading state shows structure (skeleton/progressive reveal), not only spinner.
- Error state explains what happened and gives a recovery path.

## 10) Content and copy polish

- Prefer short, specific labels and instructions.
- Replace vague CTA text ("Submit", "Continue") with contextual action text where possible.
- Keep microcopy consistent in tone and tense.
- Reduce visual noise by removing non-essential words before styling.

## 11) Enterprise SaaS density guidance

- Dense screens are acceptable when hierarchy and grouping are strong.
- Use progressive disclosure for advanced actions/settings.
- Keep destructive/high-risk actions clearly separated and confirmable.
- Preserve orientation in long workflows:
  - persistent section labels
  - visible step/state progress
  - stable action placement

## 12) Anti-patterns

- Styling shell before core feature flow is clear.
- Random visual effects without hierarchy purpose.
- Overloaded screens where all elements look equally important.
- Inconsistent icon families/weights.
- Hidden state changes with no visible feedback.
- One-off spacing/color/shadow values repeated without tokenization.

## 13) Blueprint enforcement mapping

- Variant-first:
  - key pages: 5 variants
  - low-risk pages: 3 variants
  - no implementation before human-selected variant
- UI audit:
  - hierarchy, spacing rhythm, typography, icon consistency, states, density, depth, motion
- Token discipline:
  - repeated value -> token in `docs/DESIGN_SYSTEM.md`

## Related files

- `docs/references/ui-taste-playbook-llms.txt`
- `docs/DESIGN.md`
- `docs/FRONTEND.md`
- `docs/templates/UI_PAGE_VARIANTS_TEMPLATE.md`
