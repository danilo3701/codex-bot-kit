TASK: Generate /AGENTS.md for this project.

INPUTS:
- Use FOR_AGENTS_TEMPLATE.md as the base template.
- Use the provided CONTEXT PACK and repo tree as the only source of truth.

RULES:
- Fill ALL placeholders {{...}} with concrete repo-specific values.
- Do NOT invent facts. If something is missing, ask max 3 questions and stop.
- Keep only 90%+ critical rules: workflow (PLAN→BUILD→REVIEW), ALLOWLIST, append-only tests.md, mandatory SELF-CHECK.
- Output MUST be a single file content: /AGENTS.md (final), no extra commentary.

CHECK:
- Ensure paths (modules/docs/entry points) match the repo tree.
- Ensure SELF-CHECK section requirements are included verbatim.

- The generated AGENTS.md MUST include the section "Clarity tracking (mandatory)" with:
  - Two metrics: Project Clarity % and Module Clarity %
  - Update rules (PLAN updates docs/clarity.md)
  - Build gates (80% / 85%)
