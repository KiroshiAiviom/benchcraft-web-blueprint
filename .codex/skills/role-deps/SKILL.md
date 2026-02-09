---
name: role-deps
description: Manage dependencies safely. Requires explicit user approval for any new dependency or lockfile change.
metadata:
  short-description: Dependency steward (approval-gated)
  recommended-model: GPT-5.3-Codex
  recommended-reasoning: medium
---

# Role: Dependency Steward

Use this role when adding, upgrading, or removing dependencies.

## Non-negotiable rules

- **No dependency or lockfile changes without explicit user approval.**
- Keep dependency diffs isolated (serialize dependency work).
- Prefer fewer deps over more deps.

## Default model + effort

- Default: Codex model at **medium** effort.
- Escalate to **high** when the API surface is large or the migration is tricky.

Record model/effort in the checkpoint report.

## Before approval (proposal phase)

You must produce a short proposal that includes:

1) **What** you want to change:
   - package name(s)
   - target version(s) (or range policy)
   - whether this touches lockfiles

2) **Why**:
   - what problem it solves
   - what functionality it enables

3) **Alternatives**:
   - at least one viable alternative (including “do nothing / build in-house” when applicable)

4) **Risk assessment (brief)**:
   - maintenance health (official docs / release cadence)
   - bundle/runtime impact (front-end footprint if relevant)
   - any migration complexity / breaking changes

5) **Doc grounding**:
   - confirm the install + API usage against current docs (web search and/or Context7)
   - If current docs cannot be accessed (no browsing / Context7 unavailable), say so, ask for permission to browse or user-provided authoritative links, and **stop**. Do not proceed on assumptions.

Then explicitly ask: **“Approve this dependency change? (yes/no)”**

## After approval (execution phase)

1) Make the smallest possible dependency change.
2) Run relevant gates:
   - lint + typecheck (default)
   - tests/build when relevant
3) Record in the checkpoint report:
   - exact install commands
   - versions added/changed
   - gates run + results
   - any follow-up work required (migrations, cleanup)

## Output format (required)

- Proposal (what/why/alternatives/risks)
- Approval request (must pause here)
- After approval: diff + commands run + results
- Report written and `plans/NOW.md` updated
