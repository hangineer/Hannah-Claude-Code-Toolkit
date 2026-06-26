# Hannah Claude Code Toolkit

團隊共用的 Claude Code 擴充工具箱，內含自訂的 slash command、subagent 與 skill。

## 目錄結構

- `.claude/commands/` — 自訂 slash command（檔名採 kebab-case，例如 `branch-cleanup.md`）。frontmatter 須包含 `description`，可選填 `argument-hint`、`allowed-tools`。
- `.claude/agents/` — 自訂 subagent。frontmatter 須包含 `name`、`description`、`model`。
- `.claude/skills/` — 自訂 skill，每個 skill 為 `skills/{skill-name}/` 資料夾，內含 `SKILL.md`（須包含 `name`、`description` frontmatter）。

## Commands

- `branch-cleanup` — 列出已合併或過期的本機分支並協助清理。
- `review-skill` — 呼叫 `skill-reviewer` subagent，檢查新增/修改的 command、agent、skill 是否符合慣例。
- `gitlab-code-review` — 透過 GitLab API 抓取 MR 的 diff，進行完整 code review。
- `comment-on-code-review` — 將目前對話中的 code review 結果，以你的 GitLab 帳號留言到指定 MR（支援 inline comment）。

## Agents

- `skill-reviewer` — 檢查新增/修改的 command、agent、skill 是否符合 `CLAUDE.md` 中的命名與 frontmatter 慣例。

## Skills

** 官方 **
取自 [Anthony Fu's Skills](https://github.com/antfu/skills)

- `vue` — Vue 3 Composition API、script setup macros、reactivity、內建元件（Transition/Teleport/Suspense 等）。
- `vue-best-practices` — Vue 3 最佳實踐：強推 `<script setup>` + TypeScript，涵蓋 SSR、Volar、vue-tsc。
- `vue-router-best-practices` — Vue Router 4 patterns、navigation guards、route params。
- `vue-testing-best-practices` — Vue 測試：Vitest、Vue Test Utils、component testing、Playwright E2E。
- `pinia` — Pinia 官方 state management，stores / state / getters / actions 模式。
- `vite` — Vite 設定、plugin API、SSR、Rolldown migration。
- `pnpm` — pnpm 指令、workspaces、catalogs、patches、overrides。
- `web-design-guidelines` — UI 審查：無障礙、設計規範、UX best practices。

**FET 團隊規範**

- `fet-vue3-coding-guidelines` — 依 FET 團隊規範審查 Vue 3 程式碼（命名、BEM CSS、資料夾結構、Vue 風格規則）。
- `fet-vue2-coding-guidelines` — 依 FET 團隊規範審查 Vue 2（Options API）程式碼（命名、BEM CSS、資料夾結構、Vue 風格規則）。
- `fet-code-review` — code review 入口，搭配 `fet-vue3-coding-guidelines` 使用。

**其他**

- `project-context` — 用於快速了解專案結構、技術棧與慣例。
