# Technical Spec — <Project Name>

> This document locks the technical decisions the build agent should not invent.
> Keep it **specific, versioned, and auditable**.

---

## 1) Stack (pinned)

> Fill this after you initialize the repo so versions match `package.json`/lockfile.

- Framework: Next.js <version>
- React: <version>
- TypeScript: <version>
- Package manager: Bun <version>
- UI: Tailwind CSS <version> + shadcn/ui
- Lint/format: Biome <version>
- Testing (if used): <vitest/jest/playwright> <version>

Dependency policy:

- Do not add new dependencies without explicit approval.
- When a dependency is approved, record: rationale, alternatives, and doc link.
- If dependency decisions are unresolved, surface them in thread until approved (do not persist unresolved dependency questions in this doc).

## 2) Runtime + environments

- Target runtime(s): <Node.js / Edge> (default: Node)
- Environments:
  - Local development
  - Preview (if used)
  - Production

## 3) Repository structure

- `src/app` — routes (App Router)
- `src/components` — reusable UI
- `src/lib` — utilities
- `src/server` — server-only modules (db, auth, external APIs)
- `public/` — static assets

## 4) Data + backend

> If frontend-only, keep this section short and mark DB/API as N/A.

- Database: <Postgres / Convex / N/A>
- ORM / query layer: <Drizzle / Prisma / SQL / N/A>
- Migrations: <tool / process>
- Auth: <Clerk / NextAuth / custom / N/A>

### 4.1 Schema (if applicable)

- <Table>:
  - columns:
  - constraints:
  - indexes:

### 4.2 API contracts (if applicable)

- Endpoint: `<METHOD> /api/...`
  - request:
  - response:
  - errors:

## 5) External integrations

- <Service> — purpose, auth method, rate limits, failure behavior

## 6) Environment variables

| Name | Where used | Required | Notes |
|---|---|---:|---|
| `EXAMPLE` | server | yes/no | |

## 7) Security baseline

- Never commit secrets.
- Validate user input on the server.
- Avoid exposing internal errors to the client.

## 8) Performance + UX

- SSR/CSR strategy notes:
- Caching strategy:
- Image strategy (Next Image):

## 9) Testing strategy (optional)

- Always run: lint + typecheck
- Add tests when changes are user-facing or risky.
- e2e (Playwright) for major flows only.

## 10) Deployment

- Target: <Vercel / customer infra / container>
- If containerized:
  - base image:
  - build steps:
  - runtime environment vars

## 11) Open risks

- <Risk>
