# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repo purpose

This is a team-shared toolbox of Claude Code extensions: custom slash commands, subagents, and skills. There is no application code, build step, lint, or test suite — all content is Markdown configuration files with YAML frontmatter.

## Structure

- `.claude/commands/` — custom slash commands (kebab-case filenames, e.g. `branch-cleanup.md`). Frontmatter requires `description`, may include `argument-hint`, `allowed-tools`.
- `.claude/agents/` — custom subagents. Frontmatter requires `name`, `description`, `model`.
- `.claude/skills/` — skills available to Claude Code. Each skill is a folder `skills/{skill-name}/` containing `SKILL.md` with `name` and `description` frontmatter.
- `.agents/skills/` — "universal" skills installed via the Skills CLI (`npx skills`), shared across multiple AI tools (Claude Code, Cursor, Copilot, etc.). These are symlinked into `.claude/skills/` so Claude Code can use them.
- `skills-lock.json` — lockfile tracking universal skills installed via `npx skills add` (source repo, path, content hash).

## Installing skills

Two separate mechanisms exist — don't mix them up:

- **Project-level (preferred for sharing via this repo)**: `npx skills add <owner/repo>@<skill>` — downloads the skill into `.agents/skills/`, symlinks it into `.claude/skills/`, and records it in `skills-lock.json`. Anyone who clones this repo gets the skill automatically.
- **User-level plugins** (`/plugin marketplace add ...` + `/plugin install ...`): installs into `~/.claude/plugins/`, outside this repo. Not shared by committing — each user must install separately.

## Setup for new clones

After cloning this repo, restore the universal skills tracked in `skills-lock.json`:

```bash
npx skills experimental_install
```

This re-downloads the skills into `.agents/skills/` and recreates the symlinks in `.claude/skills/`. Requires `node`/`npx`. Skills installed via `/plugin marketplace` (user-level) are not covered by this and must be installed separately per user.

## Contribution guidance

Before adding a new command/agent/skill, check whether an already-installed official plugin covers the same need (commit-commands, pr-review-toolkit, code-review, code-simplifier, code-modernization, feature-dev, hookify, ralph-loop, etc.) to avoid duplication. New tools should follow the naming/frontmatter conventions above, with a short description added to this file or the relevant directory.
