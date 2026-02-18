# Quality Score

This doc defines the checkpoint-level quality bar.
It replaces the old “Definition of Done” doc by turning it into a compact, repeatable rubric.

Use it in:

- `docs/exec-plans/active/NOW.md` (baseline)
- checkpoint reports (`reports/TEMPLATE.md`)
- PR review checklists (`.github/PULL_REQUEST_TEMPLATE.md`)

## Rating (quick, optional)

Use a simple 0–3 score in reports:

- **Q3 — Ready:** objective met, gates pass (or justified `N/A`), no obvious UX breakage.
- **Q2 — Acceptable:** objective met, minor issues or follow-ups remain, no P0.
- **Q1 — Needs changes:** missing core checks, significant risk, or visible breakage.
- **Q0 — Broken:** failing gates or functionality.

If you don’t want a number, you can still use the checklist below as pass/fail.

---

## A) Minimum bar for every checkpoint

Read-only checkpoints (docs reviews, design audits): still update `docs/exec-plans/active/NOW.md` and write a checkpoint report; mark gates as `N/A` with a reason.

1) The checkpoint objective is achieved (as written in `docs/exec-plans/active/NOW.md`).
2) `docs/exec-plans/active/NOW.md` is updated to reflect reality (checkboxes + next step).
3) No obvious breakage (when applicable):
   - the app does not crash on the basic flow,
   - no obvious runtime errors introduced by the change.
4) Quality gates (when available in the codebase):
   - `lint` passes (or `N/A` with a reason),
   - `typecheck` passes (or `N/A` with a reason),
   - `tests` pass (or `N/A` with a reason).

   Tests guidance: run tests for user-facing or risky changes; otherwise mark `tests` as `N/A` and state why in the report.
5) Changes are reviewable:
   - diff is reasonably small (or `N/A` for read-only checkpoints),
   - changes/findings are explained in a checkpoint report.
6) A checkpoint report exists in `reports/` and includes:
   - execution context (traceability),
   - commands run (or `N/A` with a reason).

---

## B) Additional bar for UI changes

1) Manual UI review completed:
   - at least one desktop viewport and one mobile viewport,
   - focus states and keyboard navigation checked.
2) Interaction states exist where applicable:
   - hover / focus / active / disabled / loading / empty / error.
3) Motion respects `prefers-reduced-motion`.
4) No obvious layout regressions across common breakpoints.

References: `docs/DESIGN.md`, `docs/FRONTEND.md`.

---

## C) Additional bar for dependency changes

1) Follow the dependency policy in `AGENTS.md` (explicit human approval required before changing dependencies/lockfiles).
2) Rationale recorded in the checkpoint report:
   - why this dependency is needed,
   - alternatives considered,
   - any relevant breaking changes.
3) Quality gates still pass (or are explicitly `N/A`).

---

## D) Additional bar for refactors

1) Refactor is driven by an explicit plan (ExecPlan or dedicated refactor doc).
2) Behavior is preserved (or behavior changes are split into a separate plan step).
3) Quality gates pass; tests are updated/added when risk warrants it.
