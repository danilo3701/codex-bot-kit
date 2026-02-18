# Telegram Bot Skeleton KIT (Codex-friendly)

Этот репозиторий — набор шаблонов и рабочих промптов для создания Telegram-ботов через Codex по процессу:
**PLAN → BUILD → REVIEW/VERIFY**.

Важно:
- Здесь нет “реального бота”. Это **KIT** (шаблоны/инструкции).
- Реальные проекты создаются в отдельном **PROJECT repo** (код + project docs).

## Быстрый старт (как пользоваться KIT)
1) Открой `kit/00_INDEX.md` — это навигация по набору.
2) Создай новый **PROJECT repo** (пустой репозиторий под конкретного бота).
3) В PROJECT repo запусти **Bootstrap PLAN** в Codex (создаст `AGENTS.md` и базовые docs).
4) Для каждого модуля: сначала PLAN (contract + tests), затем BUILD (код), затем REVIEW (узкий scope).

## Структура KIT (где что лежит)
- `kit/agent_instructions/`
  - `CONTEXT_PACK_TEMPLATE.md` — “что дать модели”, чтобы она не выдумывала
  - `FOR_AGENTS_TEMPLATE.md` — шаблон генерации проектного `AGENTS.md`
  - `GENERATE_AGENTS_PROMPT.md` — промпт генерации `AGENTS.md`
  - `FOR_DOCS_MAP.md` — политика документации (генерит `docs/docs_map.md` в проекте)

- `kit/docs_templates/`
  - `FOR_*.md` — шаблоны проектных документов (`requirements`, `runbook`, `health`, `contract`, `tests`, и т.д.)

- `kit/tasks/`
  - `CODEX_TASK_v1.md` — формат BUILD-задачи (с ALLOWLIST + DoD)
  - `CODEX_FOOTER.md` — обязательный self-check в конце каждого ответа Codex
  - `CHECK_LITE.md` — лёгкий чеклист REVIEW/VERIFY (использовать со SCOPE)
  - `FACT_CHECKING.md` — расширенная проверка (использовать только по запросу)
  - (опционально) `REVIEW_PROMPT_CHECK_LITE.md` — команда для запуска ревью по CHECK_LITE

- `kit/builders/`
  - `BOT_BUILDER_v3_2.md`, `PROMPT_IMPROVER.md` — методички/мета-процессы

## Как работаем с Codex (коротко)
### PLAN (без кода)
Цель: создать/обновить проектные документы:
- `AGENTS.md`
- `docs/docs_map.md`
- `docs/requirements.md`
- `docs/health.md`
- `docs/runbook.md`
- `modules/<module>/contract.md`
- `modules/<module>/tests.md`

Правила:
- маленькие шаги
- максимум 1–3 файла за итерацию (если можно)
- если данных не хватает — вопросы (до 3), без выдумок

### BUILD (код)
Цель: реализовать фичу строго в рамках ALLOWLIST.
В конце ответа обязательно: `SELF-CHECK` (Changed files, DoD, Manual run, Risks, If FAIL).

### REVIEW/VERIFY (узкий scope)
Цель: проверить не весь проект, а только:
- модуль (`bot/modules/<module>/...`) или
- список изменённых файлов (3–10 файлов)

Использовать `kit/tasks/CHECK_LITE.md` как чеклист.

## Contributing / изменения KIT
Рекомендуемый режим:
- изменения через branch + PR
- правим только то, что реально повышает качество (важность > 90%)
- избегаем усложнения структуры

## Security
Никогда не коммитим секреты. Используем только `.env.example` с плейсхолдерами.
