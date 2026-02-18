# CODEX ORIENT Template (Repo Navigation / Context Pull)

**Purpose:** Quickly locate where a symptom is implemented (entrypoints, data flow, dependencies) **without** writing code or refactoring.
Use this as the **first** Codex step before any fixes.

## How to use
1. Replace placeholders in **Inputs**.
2. Paste the whole prompt into Codex.
3. Enforce output format exactly.

---

## Inputs (fill these)
- **TYPE:** `BUG | FEATURE | CHANGE | QUESTION`
- **MODULE (required):** `bot/modules/<module>/`  
  *(If unknown: name the menu button / user-facing flow; Codex must infer the likely module path.)*
- **SYMPTOM (required):** `<what user sees>`
- **EXPECTED:** `<what should happen>` *(optional but helpful)*
- **REPRO STEPS:** `<steps>` *(optional)*
- **SCOPE LIMIT:**  
  - Primary: `bot/modules/<module>/`  
  - Secondary (only if needed): `bot/shared/`, `docs/`, `bot/core/` *(edit to match your repo)*

---

## Prompt to Codex (copy/paste)

You are in **ORIENT** mode. Do **not** implement changes. Do **not** refactor. Do **not** rewrite docs.
Your job is to find **where the logic lives** and map the smallest useful context.

### Task
Given:
- TYPE: {{TYPE}}
- MODULE: {{MODULE}}
- SYMPTOM: {{SYMPTOM}}
- EXPECTED: {{EXPECTED}}
- REPRO: {{REPRO STEPS}}

1) Identify the **entry points** for this module/flow (handlers/routes/commands/callbacks/menu button mapping).
2) Trace the **data flow** end-to-end for this symptom (inputs → transformations → storage → output).
3) Locate **time/tz** handling (if relevant): where timestamps are created, stored, converted, and displayed.
4) List the **minimal set of files** to read next (max 10).
5) If you truly cannot proceed, ask for **at most 1 missing detail** (e.g., module name or button label). Otherwise ask no questions.

### Scope Rules
- Stay inside: {{MODULE}}
- You may also inspect shared code only if referenced by the module:
  - `bot/shared/` / `bot/core/` / `docs/` (only when linked by imports or calls)
- Avoid scanning the entire repository.

### Output Format (must follow)
Produce exactly these sections:

1. **Quick Diagnosis (3–6 lines)**
- What is likely happening, based on code structure (no guesses without pointers).

2. **Entrypoints**
- Bullet list: file → function/class → why it matters.

3. **Flow Map**
- 5–12 bullets describing the flow: Input → processing → storage → output.
- Include time/tz points if relevant.

4. **Files to Read Next (max 10)**
- Ordered list with one-line reason each.

5. **Risks / Edge Cases**
- 3–8 bullets.

6. **One Question (only if required)**
- Ask 0–1 question. If none, write: `None`.

### Success Criteria
- I can open the “Files to Read Next” and understand where to fix without reading unrelated code.
- The list is small, relevant, and module-scoped.

---
## Notes
- If module path is unknown, infer it from naming conventions and menu/button mappings, then propose the best candidate path.
- If there are multiple candidates, list them and rank by likelihood.
