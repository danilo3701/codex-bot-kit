# <BOT_NAME> — Telegram Bot (modules-first)
Этот бот построен по принципу **modules-first**: каждая кнопка главного меню — отдельный модуль (“мини-бот внутри бота”).  
Деплой: **Railway** · Режим: **polling** · Данные: **RailwayData Volume (JSON)**.

---

## Что внутри (архитектура)
- `bot/main.py` — запуск и регистрация модулей
- `bot/config.py` — чтение ENV
- `bot/shared/` — минимум общего (подключение данных, общие кнопки при необходимости)
- `bot/modules/` — модули (ветки/мини-продукты)
  - `menu/` — главное меню (роутинг в модули)
  - `<module_name>/` — отдельная фича: handlers + keyboards + screens + contract/tests

Документация:
- `docs/requirements.md` — общий контракт проекта (ствол)
- `docs/runbook.md` — Railway/polling, логи, что делать если “молчит”
- `docs/health.md` — внутренний чеклист здоровья
- `docs/data_contract.md` — правила хранения данных в JSON
- `docs/security.md` — минимальная безопасность

---

## Быстрый старт (локально)
### 1) ENV
Скопируй пример и заполни:
- создай `.env` по `.env.example`
- укажи `BOT_TOKEN`
- укажи `DATA_PATH` (локальная папка для JSON), например `./data`

Пример:
- `BOT_TOKEN=...`
- `DATA_PATH=./data`

### 2) Запуск
Команда запуска зависит от структуры проекта, обычно:
- `python -m bot.main`

Ожидаемо:
- бот стартует без ошибок
- отвечает на `/start`
- создаёт/использует JSON-файлы в `DATA_PATH`

---

## Railway (деплой)
1) Railway → Variables:
   - `BOT_TOKEN`
   - `DATA_PATH=/data` (путь к volume)
2) Подключи Volume (RailwayData) к сервису
3) Start Command:
   - `python -m bot.main`
4) Проверь по `docs/health.md` (первые 3 блока)

---

## Данные (RailwayData / JSON)
- Данные хранятся в `DATA_PATH` в формате JSON.
- Рекомендуемая схема файлов и правила миграций описаны в `docs/data_contract.md`.

Важно:
- не дробим user-данные на 10 файлов без причины
- при битом JSON делаем backup и создаём новый пустой файл (см. data_contract)

---

## Как добавить новый модуль (кнопка = ветка)
1) Создай папку:
   - `bot/modules/<module_name>/`
2) Минимальные файлы модуля:
   - `router.py` — входы (кнопки/команды/callback)
   - `keyboards.py` — клавиатуры модуля
   - `screens.py` — тексты/рендер
   - `callbacks.py` — префиксы callback_data
   - `contract.md` — контракт модуля
   - `tests.md` — чеклист тестов модуля
3) Подключи модуль в `bot/main.py` (регистрация роутера)
4) Добавь кнопку в `bot/modules/menu/keyboards.py`
5) Прогони `docs/health.md` (smoke + nohang + clean chat)

---

## Стандарт разработки (как мы работаем с Codex)
Мы не пишем “патчи руками”. Работаем так:
1) Сначала контракт:
   - `docs/requirements.md` (если глобально)
   - `modules/<module>/contract.md` (если локально)
2) Потом чеклист:
   - `modules/<module>/tests.md`
3) Потом формируем **CODEX TASK** (границы файлов + ожидаемое поведение)
4) После изменений — прогоняем PR-Check и `docs/health.md`

---

## Troubleshooting (если что-то сломалось)
- Бот “молчит” → см. `docs/runbook.md` (чеклист по порядку)
- Кнопки “висят” (вечная загрузка) → почти всегда `answer()` в callback не вызван
- “Иногда работает” → возможно конфликт хендлеров/префиксов (DupCheck / PR-Check)
- “Данные не сохранились” → проверь `DATA_PATH` и права на запись

---

## Лицензия / заметки
(опционально)
