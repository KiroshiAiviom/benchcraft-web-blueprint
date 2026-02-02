# Definition of Done (Benchcraft Web)

This document defines when a checkpoint can be considered complete.
The goal is to prevent “massive fix-up phases” by keeping quality high at every small iteration.

---

## A) Minimum DoD for every checkpoint (15–30 minutes)

1) The checkpoint objective is achieved (as written in `plans/NOW.md`).
2) No obvious breakage:
   - the app does not crash on the basic flow (when applicable),
   - no obvious runtime errors introduced by the change.
3) Quality gates (when available in the codebase):
   - `lint` passes (or `N/A` with a reason),
   - `typecheck` passes (or `N/A` with a reason).
4) Changes are reviewable:
   - diff is reasonably small,
   - changes are explained in a checkpoint report.
5) A checkpoint report exists in `reports/` (use `reports/TEMPLATE.md`).

---

## B) Additional DoD for UI changes

1) Manual UI review completed:
   - at least one desktop viewport and one mobile viewport,
   - focus states and keyboard navigation checked.
2) Interaction states exist where applicable:
   - hover / focus / active / disabled / loading / empty / error.
3) Motion respects `prefers-reduced-motion`.
4) No obvious layout regressions across common breakpoints.

---

## C) Additional DoD for dependency changes

1) Explicit user approval obtained before changing dependencies/lockfiles.
2) Rationale recorded in the checkpoint report:
   - why this dependency is needed,
   - alternatives considered,
   - any relevant breaking changes.
3) All quality gates still pass (or are explicitly `N/A`).

---

## D) Additional DoD for refactors

1) Refactor is driven by an explicit refactor plan (`REFACTOR-*.md`).
2) Behavior is preserved (or the behavior change is split into a separate feature/bug plan).
3) Quality gates pass; tests are updated/added when risk warrants it.
