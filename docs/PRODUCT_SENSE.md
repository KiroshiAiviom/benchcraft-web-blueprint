# Product Sense

This is a lightweight set of product/UX heuristics for agent-driven development.
It helps prevent building “technically correct but unusable” features.

## Defaults

- **The Product Spec is the contract.** If a requirement isn’t written, don’t assume it.
- **Prefer the smallest shippable slice.** One clear flow beats many half-finished screens.
- **User-visible correctness > internal cleverness.** Optimize for clarity and predictability.

## UX checklist (use for most features)

- [ ] Clear primary action on each screen.
- [ ] Copy is specific (no “Lorem ipsum”, no generic button labels if it matters).
- [ ] Empty states explain what to do next.
- [ ] Errors are actionable (what happened + how to recover).
- [ ] Mobile-first layout (unless explicitly desktop-only).
- [ ] No surprise navigation or hidden state.

## Scope discipline

If scope is unclear (“make it better”, “polish”), do an **audit-only** checkpoint first:

- list 3–7 issues (P0–P3)
- propose 1–3 options
- stop for approval

(Protocol: `.codex/skills/role-ui` for UI, or a doc-audit for non-UI.)

## References

- Execution constraints + loop: `AGENTS.md`, `docs/PLANS.md`, `docs/exec-plans/active/NOW.md`
- Reliability guardrails: `docs/RELIABILITY.md`
