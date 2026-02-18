---
name: role-ui
description: Plan, audit, and implement UI/UX work using the Design + Frontend guardrails and the project Design System.
metadata:
  short-description: UI/UX guardrails + audit/build protocol
  recommended-surface: codex-app
  recommended-model: GPT-5.3-Codex
  recommended-reasoning: medium
---

# Role: UI

Use this role for **UI/UX, layout, styling, components, motion, or visual polish**.

It is designed to prevent:

- “AI-template” aesthetics
- inconsistent tokens/spacing
- wrapper-heavy DOM structure
- inaccessible focus/motion behavior

## Read-first (canonical)

- `docs/exec-plans/active/NOW.md` is the checkpoint driver. Read the files listed under **Read first**.
- Design guardrails: `docs/DESIGN.md`
- Frontend conventions: `docs/FRONTEND.md`

If `docs/DESIGN_SYSTEM.md` is missing and the UI scope is non-trivial, propose creating it from `docs/templates/DESIGN_SYSTEM_TEMPLATE.md` **before** major UI work.

## Two operating modes

### A) Audit-only (no code changes)

Use when the request is “make it look better”, “polish UI”, “review design”, or when scope is unclear.

Deliver:

- A phased plan:
  - **Phase 1 — Critical** (hierarchy, responsiveness, consistency, usability)
  - **Phase 2 — Refinement** (spacing, typography, token discipline)
  - **Phase 3 — Polish** (micro-interactions, motion, empty/loading/error states)
- A short list of **Design System updates required** (tokens/components) before implementation.
- A minimal **QA matrix**:
  - viewports to sanity check
  - focus-visible baseline
  - `prefers-reduced-motion`

Then stop and wait for approval.

### B) Build (implement approved scope)

Use when the checkpoint scope is explicit and approved.

Rules:

- Implement in **small checkpoints** (primitives → components → composition → polish).
- Do not invent new tokens. If needed, propose an update to `docs/DESIGN_SYSTEM.md` first.
- Prefer layout primitives and semantic HTML; avoid wrapper-only nesting.
- Motion must respect `prefers-reduced-motion`.

## Dependency policy

- Do not introduce new UI libraries or styling deps without explicit human approval.
- If a new dependency is needed, write a short proposal + exact commands and stop.

## Output format (end of checkpoint)

- Summary of what changed
- Files touched
- Manual UI QA checklist (what to verify in browser)
- Plan bookkeeping updated (step sheet + `EXECPLAN.md` checkboxes + `NOW.md`)
- Any approvals needed (tokens, dependencies, scope changes)
