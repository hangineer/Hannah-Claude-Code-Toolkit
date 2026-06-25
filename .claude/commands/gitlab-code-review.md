---
description: 透過 GitLab API 抓取 MR 的 diff，進行完整 code review
argument-hint: <MR_URL>
---

請依照以下步驟 review GitLab MR：

**MR URL：** $ARGUMENTS

## 步驟

1. 讀取 `~/.claude/settings.json`，取得 `mcpServers.gitlab.env` 中的 `GITLAB_PERSONAL_ACCESS_TOKEN` 和 `GITLAB_API_URL`。

2. 從 MR URL 解析出 **project path**和 **MR ID**（如 `410`）。將 project path URL encode（`/` → `%2F`）。

3. 使用 curl 呼叫 GitLab API 抓取 MR 資訊：
   ```
   GET {GITLAB_API_URL}/api/v4/projects/{encoded_path}/merge_requests/{id}
   ```
   顯示 title、author、source/target branch、description、changes count。

4. 用 curl 抓取所有變更檔案清單：
   ```
   GET {GITLAB_API_URL}/api/v4/projects/{encoded_path}/merge_requests/{id}/changes
   ```

5. 對所有變更檔案的 diff 進行分析。若變更檔案超過 5 個或 diff 總行數超過 500 行，依檔案逐批分析，每批 3–5 個檔案，全部分析完後再彙整結果。

6. 輸出結構化 review，包含：
   - **概覽**：這個 MR 做了什麼
   - **🔴 Bug / 風險**：會造成 runtime error 或邏輯錯誤的問題
   - **🟡 設計問題**：架構、命名、可維護性
   - **🟢 做得好的地方**
   - **摘要表格**：優先級、問題描述、檔案位置

審查前請讀取 `.claude/skills/code-review/SKILL.md`，依其指示載入所有相關規範（包含 Vue 3 編碼規範 `.claude/skills/vue3-project-guideline/SKILL.md` 與「做得好的地方」評估準則）。
