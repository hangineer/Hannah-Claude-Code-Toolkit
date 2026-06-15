# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repo purpose

This is a team-shared toolbox of Claude Code extensions: custom slash commands, subagents, and skills. There is no application code, build step, lint, or test suite — all content is Markdown configuration files with YAML frontmatter.

## Structure

- `.claude/commands/` — custom slash commands (kebab-case filenames, e.g. `branch-cleanup.md`). Frontmatter requires `description`, may include `argument-hint`, `allowed-tools`.
- `.claude/agents/` — custom subagents. Frontmatter requires `name`, `description`, `model`.
- `.claude/skills/` — skills available to Claude Code. Each skill is a folder `skills/{skill-name}/` containing `SKILL.md` with `name` and `description` frontmatter.

## Contribution guidance

Before adding a new command/agent/skill, check whether an already-installed official plugin covers the same need (commit-commands, pr-review-toolkit, code-review, code-simplifier, code-modernization, feature-dev, hookify, ralph-loop, etc.) to avoid duplication. New tools should follow the naming/frontmatter conventions above, with a short description added to this file or the relevant directory.
