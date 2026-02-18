MODE: PLAN (NO CODE)
GOAL: Update docs/clarity.md based on the current project documentation.

ALLOWLIST (modify ONLY):
- docs/clarity.md

INPUT RULES:
- Do not guess. If required info is missing in docs, write "НЕ ХВАТАЕТ:" and ask up to 3 questions.
- Treat "modules" as MAIN MENU BUTTON FEATURES. Each button/branch = one module.

TASK:
1) Read current docs that exist in the repo (requirements/docs_map/health/runbook and module contracts/tests if present).
2) Determine the module list:
   - Prefer explicit list from docs/requirements.md (menu buttons).
   - If not present, infer from existing module folders (modules/* or bot/modules/*).
3) For Project Clarity table:
   - Score each area 0–5 using the rubric in clarity.md.
   - Fill Notes/What’s missing.
   - Compute Project Clarity %.
   - Fill "Missing to reach 95%" (3–7 bullets).
4) For Module Clarity:
   - For each module, score Contract/Tests/Data/Edge/Integrations 0–5:
     - If contract.md exists and covers flows/data/errors/DoD → higher score.
     - If tests.md has 8–15 steps with expected results → higher score.
   - Compute Module Clarity % and write top 3 missing items.
5) Output only the updated docs/clarity.md content (no code).

OUTPUT:
- Updated docs/clarity.md
- Clarity summary: Project Clarity % + top 3 modules by lowest clarity + next PLAN suggestion
