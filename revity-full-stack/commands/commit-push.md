---
description: Commit work based on conventions and optionally push
argument-hint: [commit message hint]
allowed-tools: Bash(git *), Bash(ls), Read, Edit, Grep, Glob
---

# /commit-push

## Purpose

Commit work based on conventional commits format and then ask if ready to push.

## Contract

**Inputs:** `$ARGUMENTS` — optional hint for the commit message
**Outputs:** `STATUS=<OK|FAIL> [key=value ...]`

## Instructions

1. **Check for changes:**
   - Run `git status` to see what files have changed
   - If no changes, report and exit

2. **Review staged vs unstaged:**
   - Check `git diff --staged --stat` for staged changes
   - Check `git diff --stat` for unstaged changes
   - Check `git ls-files --others --exclude-standard` for untracked files
   - Identify which changes are ready to commit vs still pending

3. **Evaluate commit relativity:**
   - Decide: should these be one commit or split into multiple logical commits?
   - Group related changes together (same feature, same fix, same area)
   - If splitting makes sense, tell user what to stage/unstage before proceeding
   - Each commit should represent a single logical change

4. **Analyze changes:**
   - Look at the diff to understand what was modified
   - Determine the appropriate commit type based on conventions in `.claude/conventions.md`:
     - `feat:` - New features
     - `fix:` - Bug fixes
     - `docs:` - Documentation changes
     - `style:` - Code style changes
     - `refactor:` - Code refactoring
     - `perf:` - Performance improvements
     - `test:` - Adding or updating tests
     - `chore:` - Maintenance tasks
     - `ci:` - CI/CD changes
     - `build:` - Build system changes

5. **Draft commit message:**
   - Follow conventional commits format: `<type>: <description>`
   - Keep description concise (50 chars or less for subject)
   - Use imperative mood ("add feature" not "added feature")
   - Capitalize the first letter, no period at the end

6. **Show the user:**
   - Display the proposed commit message
   - Show which files will be committed
   - Ask for confirmation or changes

7. **Commit the changes:**
   - Stage all relevant files
   - Create the commit with the approved message

8. **Ask about push:**
   - Ask the user: "Ready to push to remote?"
   - If yes, run `git push`
   - If no, just confirm the commit was made locally

## Example Flow

```
User: /commit-push

Claude: I see the following changes:
- Modified: docs/1-setup.md
- Modified: docs/_config.yml
- New: docs/assets/images/revity-logo.svg

Proposed commit message:
  docs: add Revity logo and expand VS Code integration section

Does this look good? (yes/modify/cancel)

User: yes

Claude: Committed! Ready to push to origin/main? (yes/no)

User: yes

Claude: Pushed successfully!
STATUS=OK COMMIT="abc123" PUSHED=true
```

## Constraints

- Follow conventions in `.claude/conventions.md`
- Always ask before pushing (never auto-push)
- Use conventional commits format
- Never mention AI assistants in commit messages
- Keep subject line under 50 characters
- Always review staged vs unstaged before committing
- Split unrelated changes into separate logical commits
