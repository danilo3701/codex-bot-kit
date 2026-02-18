# CODEX TASK — Variant 1 (Aiogram 3 · Polling · RailwayData Volume JSON)
Дата: 2026-02-18  
Цель: создать минимально рабочий каркас Telegram-бота по **modules-first**, чтобы дальше развивать “ветка за веткой” через **MD контракты → Codex → проверки**.

---

## Входные решения (зафиксировано)
- Framework: **aiogram 3**
- Режим Telegram: **polling**
- Хранилище: **RailwayData Volume**, формат **files/JSON**, путь из ENV: `DATA_PATH`
- Clean chat строго через edit: **нет** (желательно, но не обязаловка)

---

## 0) Границы изменений (очень важно)

### Разрешено создавать/менять только
- `README.md`
- `.env.example`
- `docs/*` (requirements/runbook/health/data_contract/security/glossary)
- `bot/main.py`
- `bot/config.py`
- `bot/shared/storage.py`
- `bot/modules/menu/*`
- `bot/modules/<first_module>/*`

### Запрещено
- добавлять лишние архитектурные слои (“core/”, “managers/” и т.п.) без причины
- делать 2+ модулей одновременно
- рефакторить “на будущее”
- хранить секреты в репозитории
- трогать чужие директории/модули, которых нет в списке “разрешено”

---

## 1) Цель и результат (Acceptance)

### Должно получиться
- [ ] Бот запускается локально (polling) и отвечает на `/start`
- [ ] `/start` показывает главное меню
- [ ] В меню есть кнопка первого модуля `<first_module>`
- [ ] Нажатие кнопки открывает экран модуля
- [ ] В модуле есть навигация “Меню/Назад”
- [ ] Inline-кнопки не “висят” (callback.answer() везде)
- [ ] `DATA_PATH` создаётся/используется, есть тестовая запись/чтение JSON
- [ ] Документы созданы и короткие (10–25 строк каждый, где указано)

---

## 2) Файлы, которые нужно создать/обновить

### A) Корень репозитория
1) `README.md` (нормальный)
   - что делает бот (3–7 строк)
   - quickstart (2–6 шагов)
   - Railway деплой (ENV + start command)
   - структура modules-first
   - “How to add a module” (3–5 шагов)

2) `.env.example` (минимум)
   - `BOT_TOKEN`
   - `DATA_PATH` (локально `./data`, на Railway обычно `/data`)

---

### B) Документация (`docs/`)
Создать **короткие** файлы (10–25 строк каждый):

- `docs/requirements.md`
  - цель бота (1–3 предложения)
  - меню-модули (список кнопок)
  - глобальные UX правила (nohang, навигация)
  - non-goals
  - DoD проекта

- `docs/runbook.md`
  - Railway + polling: запуск/деплой/логи/“бот молчит”/rollback

- `docs/health.md`
  - внутренний чеклист: /start, nohang, smoke по меню и модулю, data read/write

- `docs/data_contract.md`
  - принципы JSON в volume (user-centric не дробим без нужды)
  - рекомендуемая схема файлов (users/system и т.п.)
  - schema_version + миграции
  - safe write (tmp→rename) + backup broken json

- `docs/security.md`
  - секреты (BOT_TOKEN)
  - запрет утечек в логах
  - политика ошибок пользователю vs в лог
  - запрет хранить секреты в volume json

- `docs/glossary.md`
  - 20–40 терминов (модуль, ветка, callback prefix, nohang, FormatGate и т.д.)

---

### C) Код (минимальный скелет)

1) `bot/config.py`
   - чтение env: `BOT_TOKEN`, `DATA_PATH`
   - простой объект/структура конфигурации (без бизнес-логики)

2) `bot/shared/storage.py`
   - JSON IO в `DATA_PATH`
   - гарантирует наличие папки
   - функции load/save
   - безопасная запись (желательно tmp→rename) и обработка битого JSON (backup)

3) `bot/modules/menu/`
   - `router.py` — /start + показ меню + роутинг в модули
   - `keyboards.py` — кнопки меню
   - `screens.py` — тексты/рендер меню

4) `bot/main.py`
   - создание `Bot`, `Dispatcher`
   - регистрация router’ов (menu + first_module)
   - запуск polling (aiogram 3)

---

### D) Первый модуль (заглушка по стандарту)
Если ты не указал модуль, используем дефолт:
- `<first_module>` = `settings`
- кнопка меню = “Настройки”

Создать папку: `bot/modules/<first_module>/` и файлы:
- `contract.md` — входы → шаги (2–5) → данные → edge cases
- `tests.md` — 8–15 пунктов
- `router.py` — вход из меню → экран модуля → кнопки “Назад/Меню”
- `keyboards.py`, `screens.py`, `callbacks.py`

Важно:
- сейчас делаем **один** понятный flow (без мегасистем)
- clean chat через edit — по желанию, главное: **nohang** и предсказуемая навигация

---

## 3) Мини smoke-проверка после выполнения
1) `/start` → главное меню  
2) открыть `<first_module>` → вернуться в меню  
3) выполнить действие, которое пишет/читает JSON (можно тест-кнопку внутри модуля)  
4) убедиться, что inline-кнопки не “висят” и в логах нет ошибок

---

## 4) Если информации не хватает (максимум 3 вопроса)
Если нужно уточнение, спрашивать только:
1) Как назвать `<BOT_NAME>` (для README/docs)
2) Какой именно первый модуль хочешь (если не `settings`)
3) Какой текст у кнопки первого модуля (если не “Настройки”)

---

## 5) Defaults (если я не отвечаю)
- aiogram 3 + polling
- first_module = `settings`
- кнопка = “Настройки”
- clean chat не строгий

---

# CODEX_FOOTER.md — Mandatory Self-Check & Guardrails (v1)

> Append this block to the end of EVERY CODEX_TASK you send to Codex CPI.

## 0) Hard rules (90%+)
- ✅ ALLOWLIST ONLY: modify ONLY files listed in "Allowed files".
- 🛑 If a necessary change requires a file outside ALLOWLIST: STOP and ask 1–3 questions.
- 🧪 tests.md policy: `modules/<module>/tests.md` (or project equivalent) is APPEND-ONLY:
  - you may ONLY add new test cases
  - do NOT delete old tests
  - do NOT rewrite structure "for cleanliness"
  - if a test is outdated: mark as `DEPRECATED:` and add a new correct one
- 🧠 If confidence < 90%: STOP and ask clarifying questions before further coding.

## 1) Mandatory output format (must be at the end of your response)
### SELF-CHECK
#### A) Changed files
- [ ] <file1>
- [ ] <file2>
(Only from ALLOWLIST)

#### B) DoD / Acceptance checklist
- [ ] Item 1: ...
- [ ] Item 2: ...
(Each item must be verifiable)

#### C) Manual run (no-code verification)
Provide:
- Module checklist: 8–15 steps from `.../<module>/tests.md`
- Project smoke: key steps from `docs/health.md` (start/menu/back/nohang/data read/write)
Each step must include expected result.

#### D) Risks / Regressions
List 1–3 risks + mitigation:
- Risk:
  - Mitigation:

#### E) If FAIL
If any check fails, output:
- What failed:
- Likely cause:
- Minimal fix plan (next small task) + proposed ALLOWLIST for the fix

## 2) Optional (only if requested)
- Short summary (3–6 lines) of what was implemented.
