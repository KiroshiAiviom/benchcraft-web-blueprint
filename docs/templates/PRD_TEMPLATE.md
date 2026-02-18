# PRD — <Project Name>

> Product Requirements Document. This is the **contract** for scope and “done”.
> Keep it specific. If something is not written here, the agent should not assume it.

---

## 0) Interrogation checklist (answer before coding)

- Who is this for? (1–2 primary personas)
- What is the **core action** a user takes?
- What happens on success?
- What can go wrong? (error states)
- What data is created/updated?
- Does this require authentication/roles?
- Must it work well on mobile? (usually yes)
- What is explicitly **out of scope** for v1?

---

## 1) One‑sentence summary

<One sentence describing the product and its primary user value.>

## 2) Users and context

- Primary personas:
  - <Persona 1>
  - <Persona 2>
- User goals:
  - <Goal>
- Constraints (time, compliance, customer requirements):
  - <Constraint>

## 3) Success criteria

- Measurable outcomes:
  - <Metric / KPI>
- Quality bar:
  - Must meet `docs/QUALITY_SCORE.md` for every checkpoint.

## 4) In scope / out of scope

In scope (v1):

- <Scope item>

Out of scope (v1):

- <Non-goal>

## 5) Routes + core flows (app map)

> List every route/page and the user’s navigation paths.

### 5.1 Screen inventory

| Route | Screen | Purpose | Primary action |
|---|---|---|---|
| `/` | <Home> | <What it is> | <Main CTA> |

### 5.2 Key flows

#### Flow A — <Name>

1) <Step>
2) <Step>

Success:
- <What happens>

Errors:
- <Error state> → <UI/UX behavior>

## 6) Feature list (with acceptance criteria)

> Keep features small. Prefer numbered IDs so plans can reference them.

### F1 — <Feature name>

- Problem:
  - <Why it exists>
- User story:
  - As a <persona>, I want <capability>, so that <outcome>.
- Acceptance criteria:
  - [ ] <Requirement>
  - [ ] <Requirement>
- Edge cases:
  - <Edge case>
- Notes:
  - <Implementation hint / constraints>

### F2 — <Feature name>

...

## 7) Content + copy requirements (if applicable)

- Tone:
- Required pages/sections:
- Placeholder policy:

## 8) Analytics / tracking (optional)

- Events:
- Tools:

## 9) Open questions

- <Question>

## 10) References

- Inspiration sites / patterns:
- Existing APIs / docs:
- Brand assets:
