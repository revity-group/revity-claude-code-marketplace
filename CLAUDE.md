# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Claude Code plugin marketplace containing reusable commands and skills. The marketplace registry is defined in `.claude-plugin/marketplace.json` and individual plugins live in their own directories.

## Architecture

```
.claude-plugin/marketplace.json    # Root marketplace registry listing all plugins
revity-full-stack/                 # Plugin directory
├── .claude-plugin/plugin.json     # Plugin metadata (name, version, author)
├── commands/                      # Slash command definitions (.md files)
└── skills/                        # Reusable skill definitions
```

### Command File Structure

Commands use YAML frontmatter followed by markdown instructions:

```markdown
---
description: Short description shown in command list
argument-hint: <optional-args>
allowed-tools: Bash(git status), Bash(git diff)
model: claude-haiku-4-5-20251001
---

# Command Title

<context_tag>
!`shell command to execute`
</context_tag>

## Instructions
...
```

- `allowed-tools`: Whitelist of Bash commands the command can execute
- `model`: Claude model to use (haiku for fast operations)
- `!`backtick syntax`: Executes shell commands and injects output into the prompt
- `$ARGUMENTS`: Placeholder for user-provided arguments

### Adding New Commands

1. Create a `.md` file in `revity-full-stack/commands/`
2. Add frontmatter with `description`, `allowed-tools`, and `model`
3. Write the prompt instructions with any needed context gathering

### Adding New Skills

Skills go in `revity-full-stack/skills/<skill-name>/SKILL.md` with the same frontmatter format.

## Conventions

All git-related commands follow conventional commits format:
- Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`
- Branch naming: `<type>/<short-description>`
- Commit format: `<type>(<scope>): <description>`
