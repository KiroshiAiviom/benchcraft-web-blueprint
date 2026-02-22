# Project Seed Template (`<project_seed>`)

Use this as the canonical input contract for planning.

Rules:
- Keep required fields short and concrete.
- Unknown is acceptable; write `TBD` instead of guessing.
- Prefer factual notes over polished prose.
- Provide a context dump transcript whenever possible.
- For non-functional targets, if you leave fields blank the agent should apply baseline defaults below (do not loop on these as unresolved by default).

```text
<Project Seed>

## Required (minimal)

Project name:
- <...>

One-sentence objective:
- <...>

Primary users and usage context:
- Primary user(s): <...>
- Usage context: <web / mobile web / internal tool / ...>

Core scope (must-have outcomes only):
- <...>
- <...>
- <...>

## Required input block

Context dump (freeform transcript):
- <Paste voice-to-text notes, rough thoughts, constraints, examples, and domain context.>
- <This can be messy; the agent should extract structure from it before asking follow-up questions.>

## Attached artifacts (optional but recommended)

- Technical Architecture / TA PDF: <attached / none>
- Other supporting docs (PRD, wireframes, API docs, notes): <...>
- Links/references: <...>

## Optional structure (fill only what you know)

Constraints (hard):
- Compliance/security constraints: <... or TBD>
- Data/privacy constraints: <... or TBD>
- "Do not change" constraints: <... or TBD>
- Timeline/milestones (if any): <... or N/A>

Non-functional targets:
- Performance target: <... or use default baseline>
- Reliability target: <... or use default baseline>
- Accessibility target (e.g., WCAG AA): <... or use default baseline>

Default baseline (industry-standard starting point if unspecified):
- Performance:
  - Core Web Vitals target on key routes: LCP <= 2.5s (p75), INP <= 200ms (p75), CLS <= 0.1 (p75)
  - JavaScript errors are monitored and triaged per release checkpoint
- Reliability:
  - Availability target: 99.9% monthly uptime for production user-facing paths
  - Error budget trigger: investigate if 5xx rate exceeds 1% over rolling 1h on core endpoints
- Accessibility:
  - WCAG 2.2 AA compliance target for user-facing experiences
  - Keyboard navigation + visible focus states required on all interactive flows

Tech constraints/preferences:
- Stack constraints: <... or TBD>
- Required integrations: <... or TBD>
- Environment expectations: <dev / staging / prod / TBD>

Architecture notes (optional):
- Existing backend/contracts to preserve: <...>
- Hosting/runtime constraints: <...>
- Known technical risks: <...>

Non-goals (optional):
- Explicitly out of scope for now: <...>

</Project Seed>
```

Notes for the agent:
- Extract facts from attached artifacts and context dump before broad interrogation.
- Ask as many targeted follow-up questions as needed to resolve high-impact decisions before development.
- Use baseline defaults above when those fields are omitted; only ask follow-up if stricter domain requirements are likely.
