---
description: Save current claude context conversation history by analyzing the context
argument-hint: [topic-hint]
---

# /save-history

## Purpose

Save current Claude context conversation history by analyzing the context and asking which part(s) to capture (if there are multiple points in the conversation) or if one main theme, just capture the gist and confirm before creating a markdown file.

## Contract

**Inputs:** `$ARGUMENTS` — optional topic hint for the conversation
**Outputs:** `STATUS=<OK|FAIL> PATH=<path>`

## Instructions

1. **Analyze the conversation:**
   - Review the current conversation context
   - Identify distinct topics or themes discussed
   - Note any key decisions, code changes, or solutions

2. **If multiple topics/themes:**
   - List the identified topics to the user
   - Ask: "Which part(s) would you like to capture?"
   - Allow selection of one or multiple topics

3. **If single main theme:**
   - Summarize the gist of the conversation
   - Show the proposed summary to the user
   - Ask for confirmation or modifications

4. **Generate the markdown file:**
   - Create a descriptive title (kebab-case for filename)
   - Include:
     - Date/timestamp
     - Summary of the conversation
     - Key points or decisions
     - Any relevant code snippets or commands
     - Links to files modified (if applicable)

5. **Save the file:**
   - Ensure `./conversations/` directory exists
   - Write to `./conversations/<conversation-title>.md`
   - Confirm the save location to the user

## Example Flow

```
User: /save-history

Claude: I found 2 main topics in our conversation:
1. Setting up git hooks for the plugin
2. Resolving nested git repository issue

Which would you like to capture? (1/2/both)

User: both

Claude: Here's the proposed summary:

## Git Hooks and Repository Setup
- Configured UserPromptSubmit and PreToolUse hooks
- Resolved nested .git directory issue by removing inner .git
- Committed plugin to main repository

Does this look good? (yes/modify)

User: yes

Claude: Saved to ./conversations/git-hooks-repository-setup.md
STATUS=OK PATH=./conversations/git-hooks-repository-setup.md
```

## Constraints

- Always ask for confirmation before saving
- Use kebab-case for filenames
- Include timestamp in the saved file
- Keep summaries concise but informative
