MODE: REVIEW/VERIFY
RUN: tasks/CHECK_LITE.md

SCOPE (choose one):
- Module path: <path-to-module-folder>
OR
- File list: <file1>, <file2>, <file3>
OR
- Diff summary: <paste diff/PR summary or list of changed files>

CONTEXT PROVIDED:
- Only the files/diff listed in SCOPE are in scope.
- If you need more context, ask max 3 specific file paths.

OUTPUT:
- Findings: Critical/High/Medium/Low (with evidence: file/path)
- Next small task: Goal + ALLOWLIST + DoD
- What to APPEND to .../<module>/tests.md (append-only), if needed
- Confidence % (1 line why)
