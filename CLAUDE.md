# CLAUDE.md


團隊共用的 Claude Code 擴充工具箱：自訂 slash command、subagent 與 skill。沒有應用程式碼、build 流程、lint 或測試 —— 所有內容皆為 Markdown 設定檔（搭配 YAML frontmatter）。

## 結構

- `.claude/commands/` — 自訂 slash command（檔名採 kebab-case，例如 `branch-cleanup.md`）。frontmatter 須包含 `description`，可選填 `argument-hint`、`allowed-tools`。
- `.claude/agents/` — 自訂 subagent。frontmatter 須包含 `name`、`description`、`model`。
- `.claude/skills/` — Claude Code 可使用的 skill，每個 skill 為 `skills/{skill-name}/` 資料夾，內含 `SKILL.md`（須包含 `name`、`description` frontmatter）。
