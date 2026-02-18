# 00_INDEX.md — KIT Navigation (Universal Bot Skeleton) · v2
Дата: 2026-02-18

## What this kit is
Reusable templates + prompts to **plan → build → verify** Telegram-bot projects with LLM/Codex.
Rule: **small steps only** (PLAN → BUILD → REVIEW). No “everything in one prompt”.

---

## 1) Quick Start (recommended order)
1) Fill project Context Pack:
   - `agent_instructions/CONTEXT_PACK_TEMPLATE.md`

2) Generate project-specific `/AGENTS.md`:
   - Inputs: Context Pack + repo tree + `agent_instructions/FOR_AGENTS_TEMPLATE.md`
   - Prompt: `agent_instructions/GENERATE_AGENTS_PROMPT.md`

3) Create docs policy in the target project:
   - Use `agent_instructions/FOR_DOCS_MAP.md` → output `docs/docs_map.md`

4) PLAN a feature (docs first):
   - Create/update `modules/<module>/contract.md` using `docs_templates/FOR_contract.md`
   - Create/update `modules/<module>/tests.md` using `docs_templates/FOR_tests.md`

5) BUILD in Codex (code changes):
   - Use **`tasks/CODEX_TASK_v1_WITH_FOOTER.md`** (already includes footer/guardrails)
   - Always set an ALLOWLIST (scope boundaries)

6) REVIEW/VERIFY:
   - Run `modules/<module>/tests.md`
   - Run smoke from `docs/health.md`
   - If fail → create a small next BUILD task

---

## 2) Folder map

### agent_instructions/
- `CONTEXT_PACK_TEMPLATE.md` — what to provide to LLM (facts only; no guessing)
- `FOR_AGENTS_TEMPLATE.md` — skeleton to generate real `/AGENTS.md`
- `FOR_DOCS_MAP.md` — documentation policy skeleton → `docs/docs_map.md`
- `GENERATE_AGENTS_PROMPT.md` — short prompt to generate `/AGENTS.md`

### docs_templates/
Reusable templates for target project docs:
- `FOR_README.md`
- `FOR_env.example.md` (Railway volume aware)
- `FOR_requirements.md`
- `FOR_runbook.md` (Railway + polling + replicas=1)
- `FOR_health_checklist.md`
- `FOR_glossary.md`
- `FOR_data_contract.md`
- `FOR_security.md`
- `FOR_contract.md` (module contract)
- `FOR_tests.md` (module tests checklist)
Extra (highly recommended):
- `FOR_gitignore.md`
- `FOR_requirements_txt.md`
- `FOR_callbacks_policy.md` (module callback namespace)
- `FOR_aiogram3_router_registration.md`

### tasks/
Operational prompts:
- `CHAT0_PROJECT_TASK_BUILDER.md` — converts idea → TASK PACK (context-aware)
- `CODEX_TASK_v1_WITH_FOOTER.md` — implementation task format + guardrails
- `Fact Checking.md` — verification mindset (optional)

### builders/
Meta-guides:
- `BOT_BUILDER_v3_2.md`
- `PROMPT IMPROVER.md` (optional)

---

## 3) Defaults (edit per project)
- Docs root: `docs/`
- Modules root: `bot/modules/` or `modules/` (set via repo tree)
- `tests.md` policy: append-only
- Polling rule: **replicas = 1**
- If confidence < 90% → ask questions and stop

3.1) Create "Source of Truth" policy in the target project:
   - Use `docs_templates/FOR_source_of_truth.md` → output `docs/source_of_truth.md`
   - Rule: if docs conflict, follow `docs/source_of_truth.md`

---

## 4) Canonical files (avoid duplicates)
- Use **one** canonical CODEX task:
  - ✅ `tasks/CODEX_TASK_v1_WITH_FOOTER.md`
  - ❌ `tasks/CODEX_TASK_v1.md` (deprecated; missing embedded footer)

Recommendation:
- If you keep deprecated files, mark them `DEPRECATED` at the top.
