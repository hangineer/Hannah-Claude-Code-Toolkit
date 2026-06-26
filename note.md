## 哪些東西適合放在 `~/.claude`

原則：跨專案通用放全域，專案特定留在 `.claude/`。

### 可放 `~/.claude` 的

- `keybindings.json` — 自訂快捷鍵，與專案無關
- `commands/branch-cleanup.md`
- `skills/pinia/` — 通用 Vue 狀態管理知識
- `skills/pnpm/` — 通用套件管理工具
- `skills/vite/` — 通用 build tool
- `skills/vue/` — 通用 Vue 3 語法參考
- `skills/vue-best-practices/` — 通用 Vue 最佳實踐
- `skills/vue-router-best-practices/` — 通用 Vue Router
- `skills/vue-testing-best-practices/` — 通用測試模式
- `skills/web-design-guidelines/` — 通用 UI/UX 審查
- `skills/project-context/` — 讓 Claude 讀任何專案結構的通用 skill，不是專案特定的


### 留在 repo 的 `.claude/` 的
- `skills/fet-vue2-coding-guidelines/` — 若長期在 FET 環境工作則放全域
- `skills/fet-vue3-coding-guidelines/` — 同上
- `skills/fet-code-review/` — 依賴上面兩個
- `commands/gitlab-code-review.md`
- `commands/comment-on-code-review.md`
- `commands/review-skill.md`
- `agents/skill-reviewer.md`
