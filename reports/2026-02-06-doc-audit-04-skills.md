# Doc-Audit 04 — Skills Bundle

Date: 2026-02-06  
Scope: doc-only audit of skill definitions (no edits to skill files in this checkpoint)

## Inspected files

- `.codex/skills/ui-foundation-pack/SKILL.md`
- `.codex/skills/role-builder/SKILL.md`
- `.codex/skills/role-reviewer/SKILL.md`
- `.codex/skills/role-tests/SKILL.md`
- `.codex/skills/role-deps/SKILL.md`
- `.codex/skills/role-refactor/SKILL.md`

## Findings (exactly 3 improvements)

### P1 — role-deps: explicitly handle offline / network-restricted environments

What’s wrong: `role-deps` requires “confirm … against current docs (web search and/or Context7)” but doesn’t specify what to do when network access is restricted or those tools are unavailable.

Why it matters: dependency proposals risk being based on stale/incorrect assumptions; the role also needs a deterministic “stop and ask” behavior for reproducibility and safety.

Proposed fix (small doc addition): add a short “If current docs can’t be accessed” clause:
- state the constraint (no browsing / Context7 not available),
- ask for approval to browse or request user-provided links/docs,
- otherwise stop and do not proceed with dependency changes.

### P2 — role-reviewer: require consistent, machine-actionable references (file + line)

What’s wrong: `role-reviewer` asks for “pointed to exact lines/files” but doesn’t standardize the format (and doesn’t mention the repo’s preferred file reference style).

Why it matters: reviews are slower to apply when findings are not directly navigable; line-precision reduces back-and-forth and makes “request changes” actionable.

Proposed fix (small doc addition): in “Output format” (or “What done looks like”), require each finding to include:
- `path:line` (or `path#Lline`) references when applicable,
- and a fallback when line numbers aren’t available (file + unique identifier like function/component name).

### P2 — ui-foundation-pack: tighten the “Audit-only” deliverable to include a minimum QA matrix

What’s wrong: `ui-foundation-pack` outlines phases and general deliverables, but the audit output doesn’t require a minimal verification matrix (viewports + key a11y checks) to prevent “looks good on my screen” recommendations.

Why it matters: UI polish audits often fail in responsiveness/a11y; making the audit deliverable explicitly include a small QA matrix keeps recommendations grounded and testable before build work begins.

Proposed fix (small doc addition): under “A) Audit-only”, add a short required checklist:
- viewports to sanity check (e.g., 375 / 768 / 1024 / 1440),
- focus-visible check and reduced-motion check,
- note any Design System gaps discovered during these checks.

## Quality gates

N/A (doc-only checkpoint; no code changes and no scripts affected).

