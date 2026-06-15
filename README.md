# Hannah Claude Code Toolkit

團隊共用的 Claude Code 擴充工具箱，內含自訂的 slash command、subagent 與 skill。

## 目錄結構

- `.claude/commands/` — 自訂 slash command（檔名採 kebab-case，例如 `branch-cleanup.md`）。frontmatter 須包含 `description`，可選填 `argument-hint`、`allowed-tools`。
- `.claude/agents/` — 自訂 subagent。frontmatter 須包含 `name`、`description`、`model`。
- `.claude/skills/` — 自訂 skill，每個 skill 為 `skills/{skill-name}/` 資料夾，內含 `SKILL.md`（須包含 `name`、`description` frontmatter）。

## Commands

- `branch-cleanup` — 列出已合併或過期的本機分支並協助清理。
- `review-skill` — 呼叫 `skill-reviewer` subagent，檢查新增/修改的 command、agent、skill 是否符合慣例。

## Agents

- `skill-reviewer` — 檢查新增/修改的 command、agent、skill 是否符合 `CLAUDE.md` 中的命名與 frontmatter 慣例。

## Skills

- `project-context` — 用於快速了解專案結構、技術棧與慣例。
- `vue3-project-coding-guidelines` — 依團隊規範審查 Vue 3 程式碼（命名、BEM CSS、資料夾結構、Vue 風格規則）。

## 使用方式

把 `.claude/commands/`、`.claude/agents/`、`.claude/skills/` 複製到你的專案根目錄，即可在 Claude Code 中直接使用。
