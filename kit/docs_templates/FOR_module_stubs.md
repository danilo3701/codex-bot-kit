# modules/<module>/stubs.md — Stub Registry (MVP)
Назначение: **реестр заглушек (stubs)** для одного модуля (ветки меню).  
Это “скелет решения”: мы сначала фиксируем **интерфейсы и ожидания**, потом реализуем **по одному stub’у** через цикл: tests → implement → review.

---

## 0) Как пользоваться (правило безопасности)
- 1 stub = 1 маленькая задача для Codex (ALLOWLIST 1–3 файла).
- На каждый stub: **сначала** дописать/уточнить `tests.md`, **потом** реализация, **потом** ревью.
- Если stub затрагивает общую часть (`shared/`), остановиться и написать: `НУЖНО ОБЩЕЕ: <topic>` (это отдельный stub в shared).

---

## 1) Контекст модуля (2–6 строк)
**Module name:** `<module>`  
**Menu button:** `<как называется кнопка>`  
**Purpose:** `<что делает модуль в 1 строку>`  
**Key screens:** `<экран1> → <экран2> → <экран3>`  
**Data touched:** `<какие json/ключи>`  
**Dependencies (если есть):** `<shared/time, shared/storage, другие модули>`

---

## 2) Карта потока (Happy Path, 3–7 шагов)
1) …
2) …
3) …

---

## 3) Stub List (реестр заглушек)
> Заполняй по одному. Не надо 30 штук. MVP: 5–12 stubs на модуль.

### STUB-001 — `<stub_name>`
**Статус:** `stub / implemented / verified`  
**Смысл (1 строка):** …  
**Owner file(s) (ALLOWLIST):**
- `bot/modules/<module>/...`
- `bot/shared/...` (только если реально нужно)

**Interface (черный ящик):**
- **Input:** … (что приходит: callback/action/message/state)
- **Output:** … (что должен увидеть пользователь / что записать в данные)
- **Side effects:** … (запись/чтение, отправка сообщения, изменение state)

**Rules / Constraints:**
- … (nohang, timezone, лимиты, дедлайны, “назад/меню”)

**Happy checks (3–5):**
- [ ] …
- [ ] …

**Edge checks (3–8):**
- [ ] double click
- [ ] пустой/невалидный ввод
- [ ] нет данных / файл отсутствует
- [ ] конфликт (слот занят / запись уже есть)
- [ ] …

**Test coverage link:**
- `modules/<module>/tests.md` — пункты: `<#1, #2, #7>` (номера шагов)
- (если есть) `docs/health.md` — smoke: `<что проверяется>`

**Review checklist (stub-level):**
- [ ] понятные названия и короткие функции
- [ ] nohang: callback.answer() везде где нужно
- [ ] данные не ломаются (atomic write / backup broken json)
- [ ] не трогаем файлы вне allowlist
- [ ] tests.md обновлён если поведение менялось

---

## 4) “Разрез” на файлы (если ты не программист)
> Чтобы тебе было проще, мы описываем stubs не “по файлам”, а “по действиям”.  
Потом, на этапе ORIENT, Codex сам найдёт, в каких файлах это лежит, и мы проставим allowlist.

Типовые действия (подсказка):
- Entry: открыть модуль из меню
- Render: показать экран + кнопки
- Validate: проверить ввод/правила
- Persist: записать/прочитать данные
- Transition: следующий экран/назад/меню
- Notify: опциональные уведомления

---

## 5) Definition of Done для модуля (когда можно считать “готово”)
- [ ] все stubs со статусом `verified`
- [ ] весь `modules/<module>/tests.md` проходит
- [ ] smoke из `docs/health.md` проходит
- [ ] нет изменений вне allowlist в последних задачах

---

## 6) Пример набора stubs (минимум для любого модуля)
- STUB-001: entry/open module
- STUB-002: render main screen (buttons)
- STUB-003: handle primary action (1 ключевая кнопка)
- STUB-004: persist/load data (read/write)
- STUB-005: navigation back/menu
