# Task Pack → Codex Handoff (Variant A: One Chat)

**Purpose:** Turn a user symptom into a safe, scoped Codex workflow:
1) ORIENT (find where) → 2) TASKIFY (plan & acceptance) → 3) CODEX TASK (implement)

---

## 0) What the user provides (non-technical)
- Module/button/flow name (even approximate)
- Symptom + expected behavior
- Any repro steps / frequency
- Timezone context if time-related

## 1) Chat0 output (TASK PACK)
Paste the `TASK PACK` produced by Chat0 (see `CHAT0_VOICE_INTAKE_PROMPT.md`).

## 2) Run Codex ORIENT
- Use: `CODEX_ORIENT_TEMPLATE.md`
- Fill:
  - TYPE, MODULE (or best guess), SYMPTOM
- Result:
  - Entrypoints
  - Flow map
  - “Files to read next” (max 10)

## 3) TASKIFY (no code yet)
Based on ORIENT results, produce a final mini-spec (keep it short):

```md
## TASKIFY PACK
- Goal:
- Scope (allowed paths):
- Non-goals:
- Flow (short):
- Edge cases:
- Acceptance criteria:
- Test plan:
- Allowlist files:
```

**Rule:** If acceptance changes behavior, update module canon:
- `bot/modules/<module>/contract.md`
- `bot/modules/<module>/tests.md`
*(This is your “Memory Bank” canon; avoid creating extra summary files.)*

## 4) CODEX TASK (only after user says OK)
Turn `TASKIFY PACK` into a Codex implementation task:
- Implement only within allowlist paths/files
- No refactors unless required
- Update tests (append-only when possible)
- Verify acceptance criteria

---

## Decision rule: when to write to `docs/decisions.md`
Write a decision entry when:
- You changed a global rule (time handling policy, formatting, role logic)
- You introduced a new dependency or storage format
- You changed cross-module behavior

Do **not** write decisions for:
- Small UI copy tweaks
- Minor bugfix that doesn’t change behavior outside the module
