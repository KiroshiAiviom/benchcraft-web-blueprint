# Core beliefs (agent-first development)

These beliefs are intentionally **short and stable**.
They shape how we write docs, plans, and code.

## Planning + execution

- **Repository is memory.** Do not rely on chat history.
- **Progressive disclosure.** Entry-point docs stay short; link to deeper sources.
- **One checkpoint per thread.** 15–30 minutes, reviewable diff, then stop.
- **Small diffs beat clever diffs.** Prefer incremental changes over big rewrites.

## Requirements + truth

- **Don’t invent requirements.** If unclear, record questions + assumptions, then stop.
- **Separate “what” from “how”.**
  - Product specs define *what* and acceptance criteria.
  - ExecPlans define *how* in checkpoint steps.
  - Code implements the plan.
- **Approvals are explicit.** Dependency changes and scope jumps require human approval.

## Quality

- **Quality is non-negotiable.** Use `docs/QUALITY_SCORE.md` as the rubric.
- **UI must be usable.** Keyboard navigation + focus-visible baseline + mobile layout sanity checks.
- **Security defaults to “safe”.** Validate input server-side, never leak secrets, least privilege.
- **Reliability defaults to “boring”.** Prefer predictable, observable behavior over cleverness.

## Documentation style

- **Docs are contracts, not essays.**
- Prefer:
  - short bullets
  - checklists
  - links to the single source of truth
- Avoid:
  - long prose
  - repeated rules in many places
  - huge “master docs” that try to cover everything
