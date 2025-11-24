# Revity Claude Code Marketplace

A collection of Claude Code plugins for full-stack development workflows.

## What is this?

This is a Claude Code plugin marketplace that provides productivity commands for common development tasks like branching, committing, creating PRs, and managing git worktrees—all following conventional commit standards.

## Installation

1. Open Claude Code and run the `/plugins` command
2. Select **Add marketplace**
3. Enter the repository URL:
   ```
   https://github.com/revity-group/revity-claude-code-marketplace
   ```
4. Browse and install available plugins from the marketplace

## Available Plugins

### revity-full-stack

A full-stack Next.js and React development toolkit.

**Commands:**

| Command | Description |
|---------|-------------|
| `/branch` | Create a new branch from main with conventional naming |
| `/commit` | Analyze changes and create conventional commits |
| `/push` | Commit and push changes to remote |
| `/pr` | Create a GitHub PR with formatted description |
| `/lint` | Auto-fix linting issues |
| `/save-history` | Save conversation context to markdown |
| `/worktree-create` | Create a git worktree for parallel development |
| `/worktree-cleanup` | Remove completed worktrees safely |

## Usage

After installation, exit claude code and open it again, use any command by typing it in Claude Code:

```
/revity-full-stack:branch add user authentication
/revity-full-stack:commit
/revity-full-stack:pr
```

## License

MIT
