# CLAUDE.md


團隊共用的 Claude Code 擴充工具箱：自訂 slash command、subagent 與 skill。沒有應用程式碼、build 流程、lint 或測試 —— 所有內容皆為 Markdown 設定檔（搭配 YAML frontmatter）。

## 結構

- `.claude/commands/` — 自訂 slash command（檔名採 kebab-case，例如 `branch-cleanup.md`）。frontmatter 須包含 `description`，可選填 `argument-hint`、`allowed-tools`。
- `.claude/agents/` — 自訂 subagent。frontmatter 須包含 `name`、`description`、`model`。
- `.claude/skills/` — Claude Code 可使用的 skill，每個 skill 為 `skills/{skill-name}/` 資料夾，內含 `SKILL.md`（須包含 `name`、`description` frontmatter）。

## 貢獻指南

新增 command/agent/skill 前，請先確認是否已有官方 plugin 涵蓋相同需求（commit-commands、pr-review-toolkit、code-review、code-simplifier、code-modernization、feature-dev、hookify、ralph-loop 等），以避免重複。新工具應遵循上述命名/frontmatter 慣例，並在本檔案或相關目錄中加入簡短說明。