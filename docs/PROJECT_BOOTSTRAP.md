# PROJECT_BOOTSTRAP.md — как превратить blueprint в Next.js template

> Этот файл пригодится позже, когда мы будем собирать “реальный” шаблон проекта.

## 1) Создать новый проект (Bun + Next.js)

Пример (флаги могут меняться между версиями — проверь `--help`):
```bash
bun create next-app@latest my-app \
  --typescript \
  --tailwind \
  --biome \
  --app \
  --src-dir \
  --import-alias "@/*" \
  --use-bun \
  --empty
```

## 2) Наложить Benchcraft overlay

Скопировать в корень проекта:
- `AGENTS.md`
- `.codex/`
- `docs/`
- `plans/`
- `reports/`
- `.github/` (опционально)

## 3) Инициализировать UI основу
- Настроить tokens и theme (см. `docs/UI_FOUNDATION_PACK.md`)
- Создать `docs/STYLE_GUIDE.md` из шаблона и заполнить
- Установить shadcn/ui и синхронизировать variants с tokens

## 4) Проверить workflow
- Запустить Codex (CLI/IDE), убедиться что он читает `AGENTS.md`
- Сделать первый маленький чекпоинт: “создай STYLE_GUIDE.md и базовые tokens”
