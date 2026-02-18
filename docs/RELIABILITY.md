# Reliability

Reliability means users consistently get the right outcome, with graceful failure when they don’t.
This is a compact guardrail doc for checkpoint-based development.

## Non-negotiables

- **No silent failures.** Errors must surface as:
  - clear UI error states (user-facing)
  - or clear logs/telemetry (internal)
- **Explicit states.** For every user-facing flow, account for:
  - loading
  - empty
  - error
  - success
- **Time boundaries.** Network/IO work needs timeouts/abort semantics where applicable.
- **Small diffs.** Reliability improves with reviewable, checkpointed changes.

## App Router reliability defaults (Next.js)

- Use route-level `loading.tsx` and `error.tsx` where appropriate.
- Prefer predictable data fetching and caching behavior; document it in `docs/TECH_SPEC.md`.
- Keep server-side side effects idempotent when possible (retries happen).

## Checkpoint reliability checklist

When a checkpoint touches a user flow:

- [ ] Loading and empty states exist (or explicitly `N/A`).
- [ ] Error states exist and are readable.
- [ ] The “happy path” still works.
- [ ] Typecheck and lint pass (or `N/A` with a reason).
- [ ] Risky changes have tests (or a reason why not).

## References

- Quality rubric: `docs/QUALITY_SCORE.md`
- Product expectations: `docs/PRODUCT_SENSE.md`
