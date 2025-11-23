---
description: Create a new branch from main with conventional commit-style naming
argument-hint: <task-description>
---

# /branch

## Purpose

Create a new branch from main with conventional commit-style naming.

## Contract

**Inputs:** `$ARGUMENTS` — task description for the branch
**Outputs:** `STATUS=<OK|FAIL> BRANCH=<branch-name>`

## Context

<git_status>
!`git status`
</git_status>

<current_branch>
!`git branch --show-current`
</current_branch>

<recent_branches>
!`git branch --sort=-committerdate | head -5`
</recent_branches>

## Instructions

1. **Parse the task description** from `$ARGUMENTS` to understand what needs to be done.

2. **Generate a branch name** following conventional commit style:
   ```
   <type>/<short-description>
   ```

   Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`

   Rules:
   - Lowercase only
   - Replace spaces with hyphens
   - Keep concise (3-5 words max)
   - Examples: `feat/add-dark-mode`, `fix/sidebar-scroll-issue`, `refactor/extract-utils`

3. **Switch to main and pull latest:**
   ```bash
   git checkout main && git pull origin main
   ```

4. **Create and switch to the new branch:**
   ```bash
   git checkout -b <branch-name>
   ```

5. **Confirm** with `git branch --show-current`.

6. **Output status:**
   - Print `STATUS=OK BRANCH=<branch-name>` on success
   - Print `STATUS=FAIL ERROR="message"` on failure

## Constraints

- Idempotent and deterministic
- Minimal console output (STATUS line only)
