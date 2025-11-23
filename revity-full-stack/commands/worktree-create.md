---
description: Create a new worktree following conventional commits conventions
argument-hint: [feature-description]
---

# /worktree-create

## Purpose

Create a new git worktree for parallel development following conventional commits branch naming conventions.

## Contract

**Inputs:** `$ARGUMENTS` — Natural language description of what you're working on
**Outputs:** `STATUS=<OK|FAIL> BRANCH=<branch-name> PATH=<worktree-path>`

## Instructions

1. **Read conventions:**
   - Read `.claude/conventions.md` to understand branch naming rules
   - Follow conventional commits types: feat, fix, docs, style, refactor, perf, test, chore, ci, build

2. **If no arguments provided:**
   - Ask user: "What feature or task are you working on?"
   - Wait for user response

3. **Process user input:**
   - Analyze the description to determine the type (feat, fix, docs, etc.)
   - Generate a kebab-case short description (2-4 words)
   - Construct branch name: `<type>/<short-description>`
   - Show the suggested branch name and ask for confirmation

4. **Create the worktree:**

```bash
BRANCH_NAME="<generated-branch-name>"
WORKTREE_PATH="../worktrees/$BRANCH_NAME"

# Create worktrees directory if it doesn't exist
mkdir -p "$(dirname "$WORKTREE_PATH")"

# Create worktree with new branch
git worktree add "$WORKTREE_PATH" -b "$BRANCH_NAME"

if [ $? -eq 0 ]; then
  echo "STATUS=OK BRANCH=\"$BRANCH_NAME\" PATH=\"$WORKTREE_PATH\""
else
  echo "STATUS=FAIL ERROR=\"Failed to create worktree\""
  exit 1
fi
```

5. **Output result:**
   - Print `STATUS=OK BRANCH="<name>" PATH="<path>"` on success
   - Print `STATUS=FAIL ERROR="<message>"` on failure

## Constraints

- Follow conventions in `.claude/conventions.md`
- Be conversational and ask clarifying questions
- Suggest branch names based on conventional commits
- Allow user to override suggested names

## Example Interactions

**Example 1:**
```
User: /worktree-create
Claude: What feature or task are you working on?
User: I need to add user authentication
Claude: I suggest the branch name: feat/user-authentication
       Does this look good? (yes/no or provide alternative)
User: yes
Claude: Creating worktree...
       STATUS=OK BRANCH="feat/user-authentication" PATH="../worktrees/feat/user-authentication"
```

**Example 2:**
```
User: /worktree-create fixing the login redirect bug
Claude: I suggest the branch name: fix/login-redirect
       Does this look good? (yes/no or provide alternative)
User: yes
Claude: Creating worktree...
       STATUS=OK BRANCH="fix/login-redirect" PATH="../worktrees/fix/login-redirect"
```

**Example 3:**
```
User: /worktree-create
Claude: What feature or task are you working on?
User: updating the API documentation
Claude: I suggest the branch name: docs/api-documentation
       Does this look good? (yes/no or provide alternative)
User: make it shorter
Claude: How about: docs/update-api
       Does this look good?
User: perfect
Claude: Creating worktree...
       STATUS=OK BRANCH="docs/update-api" PATH="../worktrees/docs/update-api"
```
