---
description: Create a new worktree following conventional commits conventions
argument-hint: [feature-description]
allowed-tools: Bash(git worktree:*), Bash(git branch:*), Bash(git rev-parse:*), Bash(mkdir:*)
model: claude-haiku-4-5-20251001
---

# Create Worktree

I have gathered information about your repository:

<existing_worktrees>
!`git worktree list`
</existing_worktrees>

<existing_branches>
!`git branch -a`
</existing_branches>

<current_branch>
!`git rev-parse --abbrev-ref HEAD`
</current_branch>

## Instructions

1. **If no arguments provided**, ask: "What feature or task are you working on?"

2. **Analyze the description** to determine the type and generate branch name:
   - Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`
   - Format: `<type>/<short-kebab-description>` (2-4 words)

3. **Suggest the branch name** and ask for confirmation.

4. **Create the worktree**:

```bash
mkdir -p ../worktrees
git worktree add "../worktrees/<branch-name>" -b "<branch-name>"
```

5. **Show the result** with `git worktree list` to confirm.
