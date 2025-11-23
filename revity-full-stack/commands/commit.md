---
description: Smart commit - analyze changes and create logical commits
allowed-tools: Bash(git *), Bash(ls), Read, Edit, Grep, Glob
model: Haiku
---

Analyze my git state and help me create clean, logical commits.

## Conventions

### Commit Message Format
- Use imperative mood: "Add feature" not "Added feature"
- Keep subject line under 50 characters
- Capitalize the first letter
- No period at the end of subject line
- Separate subject from body with a blank line (if body needed)

### Common Prefixes
- `feat:` new feature
- `fix:` bug fix
- `refactor:` code refactoring
- `docs:` documentation changes
- `style:` formatting, whitespace
- `test:` adding/updating tests
- `chore:` maintenance tasks

### Pushing Guidelines
- Always pull before pushing: `git pull --rebase`
- Push to feature branches, not directly to main
- Use `git push -u origin <branch>` for new branches

## Current State

**Staged changes:**
!git diff --staged --stat

**Unstaged changes:**
!git diff --stat

**Untracked files:**
!git ls-files --others --exclude-standard

## Your Task

1. Review what's staged vs unstaged
2. Decide: should these be one commit or split into multiple logical commits?
3. If splitting makes sense, tell me what to stage/unstage
4. Once we agree, write the commit message(s) following the conventions above
5. Execute the commit(s)

NOTE: always skip any mentions of Claude Code or any other AI assistant in the commit message. keep it below 50 characters and in imperative mood.
