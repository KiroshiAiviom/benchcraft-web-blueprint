---
name: ui-foundation-pack
description: Plan, audit, and implement premium UI using the UI Foundation Pack + project Design System.
metadata:
  short-description: Premium UI/UX guardrails + phased audit/build protocol.
  recommended-surface: codex-app
  recommended-model: GPT-5.3-Codex
  recommended-reasoning: medium
---

# UI Foundation Pack Skill

Use this skill when you are working on **UI/UX, layout, styling, components, motion, or visual polish**.

It is designed to prevent:

- “AI-template” aesthetics
- inconsistent spacing/tokens
- wrapper-heavy DOM structure
- inaccessible focus/motion behavior

## Read-first order

1) `plans/NOW.md`
2) `docs/PRD.md` (if present)
3) `docs/DESIGN_SYSTEM.md` (if present)
4) `docs/UI_FOUNDATION_PACK.md`
5) `docs/DOD.md`

If `docs/DESIGN_SYSTEM.md` is missing and the UI scope is non-trivial, propose creating it from `docs/templates/DESIGN_SYSTEM_TEMPLATE.md` **before** major UI work.

## Two operating modes

### A) Audit-only (no code changes)

Use when the request is “make it look better”, “polish UI”, “review design”, or when scope is unclear.

Deliver:

- A phased plan:
  - **Phase 1 — Critical** (hierarchy, responsiveness, consistency, usability)
  - **Phase 2 — Refinement** (spacing, typography, color discipline)
  - **Phase 3 — Polish** (micro-interactions, motion, empty/loading/error states)
- A short list of **Design System updates required** (tokens/components) before implementation.
- A minimal **QA matrix** for the recommendations:
  - viewports to sanity check (e.g., 375 / 768 / 1024 / 1440)
  - focus-visible baseline
  - `prefers-reduced-motion` baseline
- Stop and wait for approval.

### B) Build (implement approved scope)

Use when the checkpoint scope is explicit and approved.

Rules:

- Implement in **small checkpoints** (primitives → components → composition → polish).
- Do not invent new tokens. If needed, propose an update to `docs/DESIGN_SYSTEM.md` first.
- Prefer layout primitives (Container/Section/Stack/Grid) and **avoid wrapper-only nesting**.
- Motion must respect `prefers-reduced-motion` and be gated with `motion-safe:`.

## Minimum UI quality bar

- Typography-first: consistent scale and readable body text.
- Palette discipline: semantic tokens only; no ad-hoc hex colors for repeated values.
- Accessibility baseline:
  - WCAG AA contrast for text
  - visible focus ring (≥ 2px + offset)
  - hit targets ≥ 44×44px
  - `prefers-reduced-motion` respected

## Output format (end of checkpoint)

- Summary of what changed
- Files touched
- Manual UI QA checklist (what to verify in browser)
- Any approvals needed (tokens, dependencies, scope changes)
