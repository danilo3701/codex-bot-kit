# FOR_AGENTS_TEMPLATE.md — Universal Agent Rules Skeleton (v1)

## Purpose
This is a TEMPLATE. Your job is to generate a project-specific `/AGENTS.md`
by filling the placeholders below using the provided project context.
Do NOT invent features. If info is missing — ask 1–3 questions.

## Inputs you will receive (context pack)
- Project name & short description
- Repo tree (folders/files)
- Tech stack (if any)
- Modules list (if any)
- Critical risks (if any)

---

# AGENTS.md — Project Agent Rules (GENERATED)

## Project snapshot (fill)
- Project: {{PROJECT_NAME}}
- Domain: {{DOMAIN_SHORT}}
- Stack: {{STACK_OR_NA}}
- Entry points: {{ENTRY_POINTS_OR_NA}}
- Modules root: {{MODULES_ROOT_PATH}}
- Docs root: {{DOCS_ROOT_PATH}}

## Core workflow (mandatory)
We work in small steps:
1) PLAN: update docs/contracts/tests (NO code)
2) BUILD: implement changes (code allowed)
3) REVIEW/VERIFY: analyze changes + propose next small fix

If the task request mixes steps — ask to split.

## Safety rails (90% critical)
- Never change files outside the provided ALLOWLIST for the current task.
- If a required change is outside ALLOWLIST: STOP and ask 1–3 questions.
- If confidence < 90%: STOP and ask clarifying questions before coding.

## Allowed scope defaults (fill from repo tree)
Default allowed areas (can be tightened per task):
- Code: {{DEFAULT_CODE_PATHS}}
- Docs: {{DEFAULT_DOC_PATHS}}
Forbidden by default:
- {{FORBIDDEN_PATHS_OR_NA}}

## Docs map (source of truth)
- If the repository contains `docs/docs_map.md` (or similarly named docs map file),
  follow it as the primary documentation policy (what docs exist, when to update them).
- If no docs map exists, assume the default policy described in the kit file `FOR_DOCS_MAP.md`
  and generate `docs/docs_map.md` during PLAN when initializing a new project.

Required behavior:
- Never retrofit docs to match code in BUILD unless explicitly requested.
- Treat docs updates as PLAN work; BUILD focuses on implementation within ALLOWLIST.

## Tests policy (manual-first)
- Module tests live at: {{MODULE_TESTS_PATH_PATTERN}}
- `tests.md` is a manual checklist.
- It may be updated ONLY by appending new test cases (append-only).
- Do not rewrite structure, do not delete existing tests.

## Self-check policy (mandatory in every response)
Every final answer MUST include a "SELF-CHECK" section:
1) Changed files (list)
2) DoD/Acceptance checklist (checkboxes)
3) Manual run steps: 8–15 steps from tests.md + health smoke from docs/health.md
4) Risks/Regressions + mitigations

SCOPE RULE (mandatory):
- REVIEW/VERIFY tasks MUST specify a SCOPE (module/path or file list or diff summary).
- If SCOPE is missing: STOP and ask 1 question: "What is the review scope (module/path/files)?"
- Only review items inside SCOPE. Ignore the rest of the repository.

## Docs stability
- Health checklist: {{HEALTH_MD_PATH}}
  - Change rarely, only when a new critical risk appears.
- Contract files: {{CONTRACT_PATH_PATTERN}}
  - Updated in PLAN, not retrofitted in BUILD unless explicitly requested.

## Style
- Prefer minimal changes.
- No broad refactors unless explicitly requested.
- Keep behavior backward-compatible unless stated otherwise.
- If you propose refactor: explain benefit + risk + rollback plan.

## Open questions (only if needed)
List missing info (max 3):
- {{Q1_OR_EMPTY}}
- {{Q2_OR_EMPTY}}
- {{Q3_OR_EMPTY}}
