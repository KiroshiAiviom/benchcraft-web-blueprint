# Design

A compact set of **design/UX guardrails** for agent-driven UI work.
This is intentionally short.

- Project-specific tokens and component rules belong in `docs/DESIGN_SYSTEM.md`.
- Implementation details belong in `docs/FRONTEND.md`.

## When to read

Use this for any checkpoint that touches:

- layout / spacing / typography
- styling / theming
- components
- motion / interactions
- UX polish

## Taste invariants

- **Typography-first:** readable body text and a consistent type scale.
- **Token discipline:** if a value repeats, it becomes a token in `docs/DESIGN_SYSTEM.md`.
  - No one-off hex colors for repeated usage.
  - No “just this one spacing tweak” if it repeats.
- **Minimal DOM:** avoid wrapper-only nesting; prefer a small set of layout primitives.
- **Accessibility baseline:**
  - visible focus ring
  - touch targets ~44×44px where applicable
  - text contrast suitable for common environments
- **Motion is deliberate:** respect `prefers-reduced-motion`; avoid noisy animation.

## Anti-patterns

Avoid by default:

- generic hero + feature cards + gradient wash
- random glow/blur/noise without a clear direction
- deep `<div>` stacks used to “fix spacing”
- copying template aesthetics without an explicit design decision

## Operating modes

- **Audit-only:** when scope is unclear (“make it look better”). Produce a phased plan and stop for approval.
- **Build:** implement an approved scope in small checkpoints.

(Protocol: `.codex/skills/role-ui`.)

## QA baseline

- Viewports: 375×812, 768×1024, 1024×768, 1440×900
- Keyboard: tab through controls; focus always visible
- Reduced motion: verify with `prefers-reduced-motion`

## How to request UI work (prompt formula)

Keep it short and structured:

1) Context: what screen/flow and what problem.
2) Constraints: design system/tokens, no new deps, must be mobile-first, etc.
3) Ask for either:
   - **Audit-only** (plan + recommendations), or
   - **Build** (implement the next small step).
