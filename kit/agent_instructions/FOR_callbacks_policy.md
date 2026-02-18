# FOR_callbacks_policy.md — Callback Namespace Policy (aiogram 3 · modules-first)

## Цель
Избежать конфликтов callback_data между модулями и сделать роутинг предсказуемым.

---

## 1) Обязательное правило
**Каждый модуль имеет свой namespace (prefix).**

Формат (рекомендуемый):
- `<module>:<action>:<payload>`
Примеры:
- `settings:open`
- `settings:tz:set:Asia/Tokyo`
- `slots:book:confirm:12345`

---

## 2) Где хранить
В каждом модуле должен быть файл:
- `bot/modules/<module>/callbacks.py`

И там:
- `PREFIX = "<module>"`
- перечисление “actions” (строки/константы)
- функции-сборщики callback_data (если нужно)

---

## 3) Фильтрация в router.py (идея)
В `router.py` модуля обрабатываем только свои callbacks:
- по `PREFIX`
- по `action`

**Запрет:** общий handler на “всё подряд” внутри модуля.

---

## 4) Ограничения payload
- payload должен быть коротким
- payload не должен содержать секреты
- если payload = id, то только id (без персональных данных)

---

## 5) Тесты (что проверять в tests.md)
Минимум:
- [ ] все inline-кнопки используют правильный prefix
- [ ] кнопки другого модуля не вызывают этот модуль
- [ ] nohang: callback.answer() везде
- [ ] double click не создаёт дублей

---

## 6) Вставка в contract.md (готовый блок)
Добавляй в `modules/<module>/contract.md`:

**Callback prefix’ы:**
- `<module>` — все callbacks этого модуля

**Callback actions:**
- `open` — открыть экран
- `back` — назад
- `menu` — в меню
- … (остальные)

---

## 7) Definition of Done (callbacks)
- [ ] у модуля есть `callbacks.py`
- [ ] все callbacks строго в namespace модуля
- [ ] нет конфликтов prefix между модулями
