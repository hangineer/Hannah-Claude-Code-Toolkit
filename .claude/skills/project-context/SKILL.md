---
name: project-context
description: Use when the user asks to "introduce this project," "what does this project do," "help me understand this repo," or at the start of a new conversation when a quick overview of the project structure, tech stack, and conventions is needed.
version: 0.1.0
---

# Project Context

## Goal

Quickly summarize the project's structure, tech stack, and development conventions to help the user (or a new collaborator) get up to speed on the project as fast as possible.

## Steps

1. **Basic info**: Read `README.md` and `CLAUDE.md` (if present) to understand the project's purpose and existing documentation.
2. **Tech stack**: Check dependency manifest files (e.g. `package.json`, `pyproject.toml`, `go.mod`, `Cargo.toml`, etc.) and list the main languages, frameworks, and key dependencies.
3. **Directory structure**: List the project's main directories (about 2-3 levels deep, excluding `.git`, `node_modules`, `dist`, `build`, etc.) and briefly describe each directory's purpose.
4. **Development conventions**:
   - Check for lint/format configs (e.g. `.eslintrc`, `.prettierrc`, the `[tool.ruff]` section in `pyproject.toml`, etc.)
   - Check the testing framework and test directory locations
   - Check `.claude/` for custom commands, agents, and skills, and briefly describe their purpose
5. **Recent activity**: Run `git log --oneline -10` to understand the direction of recent changes.

## Output format

Present the summary as a bulleted list with the following structure:

- **Project overview**: one or two sentences describing what this project is
- **Tech stack**: languages, frameworks, key dependencies
- **Directory structure**: main directories and their purposes
- **Development conventions**: lint/format/testing conventions, contents of the Claude toolbox
- **Recent activity**: direction of recent commits

The summary should be concise and avoid listing file contents line by line; if the user wants to dive deeper into a specific part afterward, refer to the corresponding file.
