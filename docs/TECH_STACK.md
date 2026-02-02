# TECH_STACK.md — Benchcraft Web baseline

Это “база” для большинства проектов (SaaS/enterprise web).

## Baseline (фиксируем)
- Framework: **Next.js** (App Router)
- Language: **TypeScript**
- Package manager / runner: **Bun**
- Styling: **Tailwind CSS**
- Component baseline: **shadcn/ui** (с кастомизацией под STYLE_GUIDE + tokens)
- Lint / format: **Biome** (где уместно)
- Deployment: varies (Vercel для личного, иначе инфраструктура заказчика)
- Docker: часто нужен для enterprise (локальные сервисы / совместимость окружений)

## Varies per-project (не фиксируем заранее)
- Database: Postgres / Convex / …
- ORM / query: зависит от проекта
- Auth: зависит от проекта
- E2E: по размеру изменений/рискам

## Non-goals
- Vite-based templates
