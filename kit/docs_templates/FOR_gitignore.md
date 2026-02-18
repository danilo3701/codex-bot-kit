# FOR_.gitignore.md — Template

```gitignore
# .gitignore (template)
# Secrets
.env
.env.*
!.env.example

# Local data (Railway Volume local equivalent)
data/
*.db
*.sqlite
*.sqlite3
*.log

# Python cache
__pycache__/
*.pyc
*.pyo
.pytest_cache/
.mypy_cache/
.ruff_cache/

# OS / IDE
.DS_Store
Thumbs.db
.vscode/
.idea/

# Build artifacts
dist/
build/
*.egg-info/
```
