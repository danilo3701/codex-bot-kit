# CODEX_FOOTER.md — Mandatory Self-Check & Guardrails (v1)

> Append this block to the end of EVERY CODEX_TASK you send to Codex CPI.

## 0) Hard rules (90%+)
- ✅ ALLOWLIST ONLY: modify ONLY files listed in "Allowed files".
- 🛑 If a necessary change requires a file outside ALLOWLIST: STOP and ask 1–3 questions.
- 🧪 tests.md policy: `modules/<module>/tests.md` (or project equivalent) is APPEND-ONLY:
  - you may ONLY add new test cases
  - do NOT delete old tests
  - do NOT rewrite structure "for cleanliness"
  - if a test is outdated: mark as `DEPRECATED:` and add a new correct one
- 🧠 If confidence < 90%: STOP and ask clarifying questions before further coding.

## 1) Mandatory output format (must be at the end of your response)
### SELF-CHECK
#### A) Changed files
- [ ] <file1>
- [ ] <file2>
(Only from ALLOWLIST)

#### B) DoD / Acceptance checklist
- [ ] Item 1: ...
- [ ] Item 2: ...
(Each item must be verifiable)

#### C) Manual run (no-code verification)
Provide:
- Module checklist: 8–15 steps from `.../<module>/tests.md`
- Project smoke: key steps from `docs/health.md` (start/menu/back/nohang/data read/write)
Each step must include expected result.

#### D) Risks / Regressions
List 1–3 risks + mitigation:
- Risk:
  - Mitigation:

#### E) If FAIL
If any check fails, output:
- What failed:
- Likely cause:
- Minimal fix plan (next small task) + proposed ALLOWLIST for the fix

## 2) Optional (only if requested)
- Short summary (3–6 lines) of what was implemented.
