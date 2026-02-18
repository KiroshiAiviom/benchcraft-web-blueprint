# Architecture

This document is a **map**, not a spec.
Keep it short (ideally **1–2 pages**) and link out to deeper docs.

- Product specs (scope + AC): `docs/product-specs/`
- Technical decisions: `docs/TECH_SPEC.md`
- Frontend conventions: `docs/FRONTEND.md`
- Design decisions (optional): `docs/design-docs/`
- Reliability & security guardrails: `docs/RELIABILITY.md`, `docs/SECURITY.md`

---

## System overview (fill in per project)

- What are we building (one sentence):
- Primary users/personas:
- Core flows (link product spec section):
- Environments: local / staging / prod
- Hosting/deploy target (e.g., Vercel, internal):

## Baseline architecture principles (repo-wide)

- **Small, composable boundaries.** Prefer a few stable modules over many tiny abstractions.
- **Server authority.** Auth/authz, data validation, and side effects are enforced server-side.
- **Progressive disclosure.** Keep entry-point docs short; link to details.
- **Reviewable change.** One checkpoint = one small diff = one report.

## Boundaries and dependency rules (default)

A simple mental model:

- **UI layer**: components, styling, view composition.
- **Domain layer**: use-cases, business rules, validation.
- **Data layer**: DB/external APIs, persistence, caching.
- **Infra/ops**: config, deployment, observability.

Default dependency direction:

`UI → Domain → Data` (avoid back-edges)

Rules of thumb:

- UI should not directly import DB/infra modules.
- Domain code should be testable without the UI.
- Data layer should keep external concerns (SDKs, SQL) contained.

## Next.js App Router conventions (baseline)

- Route ownership lives in `app/`.
- Prefer colocating UI per route (route-level components) while keeping reusable primitives in `components/`.
- Put cross-cutting helpers in `lib/`.

(Details: `docs/FRONTEND.md`.)

## Decision records

When a decision is high-impact or hard to reverse, write a short design doc:

- `docs/design-docs/YYYY-MM-DD--<slug>.md`

Then link it here (and from the relevant product spec / ExecPlan).
