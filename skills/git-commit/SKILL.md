---
name: git-commit
description: Git commit workflow for Claude Code. Use when asked to commit, stage, or create git commits. Enforces 50-char limit, conventional commit prefixes, feature-based atomic commits, and excludes spec/config files from staging.
---

# Git Commit Skill

## Commit Rules

1. **Message format**: `<prefix>: <description>` (max 50 chars total, no newlines)
2. **Atomic commits**: One logical change per commit
3. **Excluded paths** (never stage, keep untracked):
   - `specs/`, `spec.md`, `CLAUDE.md`
   - `.specify/`, `.claude/`, `.auto-claude/`

## Prefix Reference

| Prefix | Use case |
|--------|----------|
| `feat` | New feature |
| `fix` | Bug fix |
| `refactor` | Code restructure (no behavior change) |
| `docs` | Documentation only |
| `style` | Formatting (no code change) |
| `test` | Adding/updating tests |
| `chore` | Build, config, dependencies |
| `perf` | Performance improvement |

## Workflow

```bash
# 1. Check status
git status

# 2. Stage files (exclude spec/config paths)
git add <files>  # Never: specs/ spec.md CLAUDE.md .specify/ .claude/ .auto-claude/

# 3. Commit with prefix
git commit -m "<prefix>: <description>"
```

## Examples

```bash
git commit -m "feat: add user authentication endpoint"
git commit -m "fix: resolve null pointer in parser"
git commit -m "refactor: extract validation logic"
git commit -m "docs: update API usage examples"
git commit -m "chore: upgrade axios to v1.6.0"
```

## Multi-feature Changes

When changes span multiple features, split into separate commits:

```bash
# Bad: one commit for unrelated changes
git add .
git commit -m "feat: add login and fix bug and update docs"

# Good: atomic commits
git add src/auth/
git commit -m "feat: add JWT authentication"

git add src/parser.js
git commit -m "fix: handle empty input in parser"

git add README.md
git commit -m "docs: add authentication section"
```
