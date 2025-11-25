---
description: Pick specific files from another branch or commit
argument-hint: <branch-or-commit>
allowed-tools: Bash(git status), Bash(git branch), Bash(git log), Bash(git show), Bash(git diff), Bash(git checkout), Bash(git restore)
model: claude-haiku-4-5-20251001
---

# Cherry-Pick Files

## Context

<git_status>
!`git status`
</git_status>

<current_branch>
!`git branch --show-current`
</current_branch>

<recent_branches>
!`git branch --sort=-committerdate | head -10`
</recent_branches>

## Source

$ARGUMENTS

## Instructions

### Step 1: Identify the source

1. **Parse the source** from `$ARGUMENTS` above:
   - If it's a branch name (e.g., `feat/user-auth`), use the latest commit from that branch
   - If it's a commit hash (e.g., `a1b2c3d`), use that commit directly
   - If empty, ask the user which branch/commit to pick from

### Step 2: Show available files

2. **Show what changed** in that commit:
   ```bash
   git show --name-status <commit-or-branch>
   ```

3. **List the files** clearly so the user can see what's available to pick.

### Step 3: Ask which files to pick

4. **Ask the user** which specific files they want to cherry-pick from the list above.
   - They can specify multiple files separated by spaces
   - They can use paths relative to repo root

### Step 4: Cherry-pick the files

5. **For each selected file**, grab it from the source:
   ```bash
   git checkout <commit-or-branch> -- <file-path>
   ```

   This will:
   - Copy the file from that commit into your working directory
   - Automatically stage the change

6. **Show what was picked**:
   ```bash
   git status
   git diff --cached --stat
   ```

### Step 5: Confirm

7. **Summarize** what files were picked and from where.

8. **Remind the user** they can now:
   - Review the changes with `git diff --cached`
   - Commit with `/commit`
   - Or unstage with `git restore --staged <file>` if they changed their mind

## Examples

```bash
# Pick from a branch
/cherry-pick feat/dark-mode

# Pick from a specific commit
/cherry-pick a1b2c3d

# Pick from main
/cherry-pick main
```
