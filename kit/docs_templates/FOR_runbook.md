# FOR_runbook.md — Runbook Template (v2 · Railway + Polling + Volume)

## 1) Коротко: как устроен запуск
- Платформа: Railway
- Режим Telegram: **polling**
- Данные: **Railway Volume** (files/JSON), путь: `DATA_PATH`

## 2) Важные правила (критично)
### 2.1 Polling = один инстанс
- **Нельзя** запускать 2+ реплики/инстанса с polling на один `BOT_TOKEN`.
- Railway Scaling/Replicas должны быть **1**, иначе будут конфликты (бот будет “падать/ругаться”).
- Если нужен масштаб — переходить на webhook (это отдельная задача).

### 2.2 Volume path (DATA_PATH)
- Volume в Railway монтируется в конкретную папку (mount path).
- Railway часто даёт переменную `RAILWAY_VOLUME_MOUNT_PATH` (если Volume подключён).
- Рекомендуемо: `DATA_PATH=$RAILWAY_VOLUME_MOUNT_PATH`
- Локально: `DATA_PATH=./data`

## 3) Локальный запуск (быстро)
- Создай `.env` по `.env.example`
- Укажи `BOT_TOKEN`
- Укажи `DATA_PATH=./data`
- Запусти команду проекта (пример): `python -m bot.main`

Ожидаемо:
- бот отвечает на `/start`
- папка `DATA_PATH` создаётся (если её не было)
- JSON-файлы читаются/пишутся без ошибок

## 4) Railway деплой (чеклист)
- Variables:
  - `BOT_TOKEN`
  - `DATA_PATH` (mount path volume или `$RAILWAY_VOLUME_MOUNT_PATH`)
- Volume:
  - подключён к сервису
  - проверен mount path
- Scaling:
  - replicas = **1**
- Logs:
  - есть “start/polling started”
  - нет циклов рестарта

## 5) Если бот “молчит” (по порядку)
1) Логи: есть ли ошибка токена/импорта?
2) Polling стартовал?
3) Replicas = 1?
4) DATA_PATH доступен на запись?
5) JSON не повреждён? (JSONDecodeError)

## 6) Rollback
- Railway: redeploy предыдущий успешный деплой
- После отката: пройти smoke (см. `docs/health.md`)
