# docs/stubs_rules.md — Stub Workflow Rules (MVP)
Цель: единый процесс “декомпозиция → stubs → tests → implement → review”.

## 1) Когда создавать stubs
- для любой новой фичи/модуля
- для сложного бага, который требует 2+ шагов

## 2) Правило 1 stub = 1 Codex task
Каждый stub реализуется отдельно:
- ALLOWLIST 1–3 файла
- маленький DoD (5–10 галочек)
- маленький tests.md (8–15 шагов)

## 3) Порядок работ
1) Обновить `modules/<module>/stubs.md` (добавить/уточнить stub)
2) Обновить `modules/<module>/tests.md` (тесты-фильтры под stub)
3) Codex: реализовать stub по allowlist
4) Review: прогнать tests.md + smoke + чеклист
5) Отметить stub `verified`

## 4) Что считается “общим” (shared stubs)
Если stub затрагивает 2+ модулей:
- создать stub в `memory/shared/<topic>.md` (или `bot/shared/` контракт)
- реализовать shared stub отдельно
- только потом возвращаться в модуль

## 5) Не делать
- не реализовывать 2 stubs одним большим коммитом
- не “заодно” рефакторить другие модули
- не добавлять новые зависимости без фиксации в requirements
