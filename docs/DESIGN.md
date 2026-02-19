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
- **Spacing rhythm first:** use a consistent spacing scale and stable vertical rhythm.
  - Prefer `gap` in flex/grid stacks over ad-hoc vertical margins.
  - Avoid relying on collapsing margins for layout spacing.
- **Minimal DOM:** avoid wrapper-only nesting; prefer a small set of layout primitives.
- **Accessibility baseline:**
  - visible focus ring
  - touch targets ~44×44px where applicable
  - text contrast suitable for common environments
- **Motion is deliberate:** respect `prefers-reduced-motion`; avoid noisy animation.

## UI feedback loop (required for UI checkpoints)

For UI work, do not stop at “code compiles.”

1) Implement with tokens + primitives.
2) Render and review at required viewports.
3) Run a UI audit (manual today; automated visual diffs when available).
4) Patch any visual consistency issues before checkpoint handoff.

## UI audit contract

Every UI checkpoint should include a short audit summary in the report:

- Spacing: list unique spacing values used for margin/padding/gap and confirm they map to the project spacing scale.
- Typography: list type tokens/styles used and confirm a consistent hierarchy.
- Accessibility quick checks: focus-visible, keyboard traversal on primary flow, contrast sanity check.
- States: confirm required interaction states exist (hover/focus/active/disabled/loading/empty/error where applicable).
- Responsive sanity: note desktop + mobile viewport checks and any intentional exceptions.

## Anti-patterns

Avoid by default:

- generic hero + feature cards + gradient wash
- random glow/blur/noise without a clear direction
- deep `<div>` stacks used to “fix spacing”
- random one-off spacing/color values scattered across pages
- copying template aesthetics without an explicit design decision

## Operating modes

- **Audit-only:** when scope is unclear (“make it look better”). Produce a phased plan and stop for approval.
- **Build:** implement an approved scope in small checkpoints.

(Protocol: `.codex/skills/role-ui`.)

## QA baseline

- Viewports: 375×812, 768×1024, 1024×768, 1440×900
- Keyboard: tab through controls; focus always visible
- Reduced motion: verify with `prefers-reduced-motion`
- Capture evidence: include before/after screenshots for UI-impacting checkpoints when practical

## How to request UI work (prompt formula)

Keep it short and structured:

1) Context: what screen/flow and what problem.
2) Constraints: design system/tokens, no new deps, must be mobile-first, etc.
3) Ask for either:
   - **Audit-only** (plan + recommendations), or
   - **Build** (implement the next small step).
