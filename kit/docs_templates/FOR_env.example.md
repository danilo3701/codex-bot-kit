# FOR_env.example.md — .env.example Template (v2 · Railway Volume aware)

> Цель: стандартный `.env.example`, который работает локально и на Railway.

```env
# Telegram
BOT_TOKEN=1234567890:REPLACE_WITH_REAL_TOKEN

# Data path (Volume / Local)
# Local: ./data
# Railway (рекомендуется): использовать путь монтирования Volume
# Railway sets RAILWAY_VOLUME_MOUNT_PATH when a Volume is attached.
# Example: DATA_PATH=$RAILWAY_VOLUME_MOUNT_PATH
DATA_PATH=./data

# Optional (если нужно позже)
# LOG_LEVEL=INFO
# TZ=UTC
```

## Примечания
- **Не коммить реальные токены**. В репо только `.env.example`.
- На Railway: подключи Volume → посмотри mount path → выставь `DATA_PATH` в Variables.
- Если используешь `RAILWAY_VOLUME_MOUNT_PATH`, убедись, что переменная доступна в твоём сервисе.
