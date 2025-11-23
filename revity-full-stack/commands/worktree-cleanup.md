---
description: Intelligently remove completed worktrees by checking PR status, uncommitted changes and branch merge status
allowed-tools: Bash(git worktree:*), Bash(git branch:*), Bash(git status:*), Bash(git log:*), Bash(gh pr:*), Bash(rm:*)
model: claude-haiku-4-5-20251001
---

# Worktree Cleanup

I have gathered information about your worktrees:

<existing_worktrees>
!`git worktree list`
</existing_worktrees>

<main_branch>
!`git rev-parse --abbrev-ref origin/HEAD 2>/dev/null | sed 's|origin/||' || echo "main"`
</main_branch>

## Instructions

1. **For each worktree** (excluding the main working directory), check:

   a. **Uncommitted changes** — Run `git -C <worktree-path> status --porcelain`
   b. **PR status** — Run `gh pr view <branch-name> --json state,merged -q '.state + " " + (.merged | tostring)'`
   c. **Merge status** — Run `git branch --merged <main-branch> | grep <branch-name>`

2. **Categorize each worktree**:
   - **Safe to remove**: PR merged/closed AND no uncommitted changes AND branch merged
   - **Needs attention**: Has uncommitted changes OR open PR
   - **Manual review**: Unable to determine status

3. **Present a summary table** showing each worktree with its status.

4. **Ask for confirmation** before removing any worktrees.

5. **Remove approved worktrees**:

   ```bash
   git worktree remove <worktree-path>
   git branch -d <branch-name>
   ```

6. **Show the result** with `git worktree list` to confirm cleanup.
