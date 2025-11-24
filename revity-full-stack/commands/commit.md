---
description: Create a conventional commit message and commit staged changes
allowed-tools: Bash(git status), Bash(git diff), Bash(git log), Bash(git add), Bash(git commit)
model: claude-haiku-4-5-20251001
---

# Conventional Commit

<git_status>
!`git status`
</git_status>

<staged_diff>
!`git diff --cached`
</staged_diff>

<unstaged_diff>
!`git diff`
</unstaged_diff>

<recent_commits>
!`git log --oneline -5`
</recent_commits>

## Instructions

Stage all changes and commit. Use conventional commit format:

```text
<type>(<scope>): <description>
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`

If changes are unrelated, split into a few logical commits. Otherwise, one commit is fine.

Never mention AI / Claude in the commit message.

```bash
git add -A && git commit -m "type(scope): description"
```
