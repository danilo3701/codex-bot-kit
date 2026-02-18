# FOR_clarity.md — Template to generate docs/clarity.md (v1)
Purpose: Generate a project-specific `docs/clarity.md` that tracks readiness to BUILD.
Rule: Do not invent. If info is missing — write `НЕ ХВАТАЕТ:` and ask max 3 questions.

Assumptions:
- "Module" = one MAIN MENU BUTTON / branch (e.g., Vocabulary, Grammar, Podcasts, Settings).
- Also track "Service modules" (Navigation/State, Storage/Data, Admin) as separate rows.

---

# Clarity Dashboard (v1)
Цель: фиксировать “насколько понятно” по проекту и по каждому модулю (кнопке меню),
чтобы понимать, когда можно переходить из PLAN в BUILD.

## 0) Как считаем % (простой и одинаковый способ)
Шкала для каждого пункта:
- 0 = нет информации
- 1 = очень расплывчато
- 2 = есть идея, но много дыр
- 3 = достаточно, чтобы начать
- 4 = хорошо, риск низкий
- 5 = отлично, почти без вопросов

Перевод в проценты:
- % раздела = (сумма баллов / максимум) * 100
- Project Clarity % = среднее по таблице Project Clarity
- Module Clarity % = среднее по колонкам (Contract/Tests/Data/Edge/Integrations)

## 1) Gates (когда можно BUILD)
- Project Clarity >= 80%  → можно начинать BUILD для первого модуля
- Module Clarity >= 85%   → можно BUILD именно этот модуль
Если ниже → продолжаем PLAN и закрываем “Missing”.

---

## 2) Project Clarity (общая картина)
Заполняется на BOOTSTRAP PLAN и обновляется при изменениях требований.

| Area | Score (0-5) | Notes / What’s missing |
|---|---:|---|
| Purpose & Users (цель, аудитория) | 0 | |
| Core Flows (3–5 главных сценариев) | 0 | |
| Menu / Module Map (кнопки меню + границы) | 0 | |
| UX Rules (no-hang, clean chat, меню/назад) | 0 | |
| Data/Storage choice (JSON/DB/Sheets, где хранится) | 0 | |
| Security basics (секреты, PII, логи) | 0 | |
| Ops/Runbook (как запускать/чинить) | 0 | |
| Definition of Done (как понять “готово”) | 0 | |

**Project Clarity %:** ___%

**Missing to reach 95% (3–7 bullets):**
- [ ] …
- [ ] …
- [ ] …

---

## 3) Module Clarity (по кнопкам меню / веткам)
Каждый модуль оцениваем отдельно: контракт + тесты + данные + edge cases + интеграции.

### 3.1 Таблица по модулям
(Добавь реальные названия кнопок меню. Если модули ещё не определены — оставь 3–6 строк-заглушек.)

| Module (menu button) | Contract (0-5) | Tests (0-5) | Data/State (0-5) | Edge/Errors (0-5) | Integrations (0-5) | Module Clarity % | Missing (top 3) |
|---|---:|---:|---:|---:|---:|---:|---|
| Navigation & State (service) | 0 | 0 | 0 | 0 | 0 | ___% | … |
| Storage/Data (service) | 0 | 0 | 0 | 0 | 0 | ___% | … |
| Admin/Moderation (service, if any) | 0 | 0 | 0 | 0 | 0 | ___% | … |
| <module_1> | 0 | 0 | 0 | 0 | 0 | ___% | … |
| <module_2> | 0 | 0 | 0 | 0 | 0 | ___% | … |
| <module_3> | 0 | 0 | 0 | 0 | 0 | ___% | … |

### 3.2 Что значит “Contract=4–5”
- Чёткие входы/выходы (что видит пользователь)
- Шаги/ветки (основной flow)
- Данные/состояния (что читаем/пишем)
- Ошибки и edge cases
- DoD (как проверить готовность)

### 3.3 Что значит “Tests=4–5”
- В `modules/<module>/tests.md` есть 8–15 шагов
- У каждого шага есть ожидаемый результат
- Есть негативные кейсы (ошибки/повторы/пусто)
- append-only соблюдается (не удаляем/не переписываем структуру)

---

## 4) Update rules (как поддерживать)
- После BOOTSTRAP PLAN: заполнить Project Clarity + создать список модулей (кнопок меню).
- После PLAN каждого модуля: обновить строку модуля + “Missing (top 3)”.
- После REVIEW: если нашли пробел — добавить его в Missing и/или понизить оценку.

---

## 5) Anti-hallucination (обязательно)
Если чего-то нет в документах:
- написать `НЕ ХВАТАЕТ:` + конкретные пробелы
- задать максимум 3 вопроса
- не выдумывать
