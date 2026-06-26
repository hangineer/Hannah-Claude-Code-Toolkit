---
description: 將目前對話中的 code review 結果，以你的 GitLab 帳號留言到指定 MR（支援 inline comment）
---

請依照以下步驟，將 review 結果留言到 GitLab MR：

**MR URL：** $ARGUMENTS

## 留言語氣

撰寫留言內容（步驟 5、6 的 `body`）時，口吻須正向積極，避免情緒化或衝動的表達。

- 反面範例：「這邊寫法很糟糕，可讀性很差，特定 magic number 應該抽出來，之前不是說過不要這樣寫嗎？」

## 步驟

### 1. 讀取設定
讀取 `~/.claude/settings.json`，取得 `mcpServers.gitlab.env` 中的 `GITLAB_PERSONAL_ACCESS_TOKEN` 和 `GITLAB_API_URL`。

### 2. 解析 MR URL
從 URL 解析出 project path（如 `human-resource/epad/epad-vue`）和 MR ID（如 `410`），將 project path URL encode（`/` → `%2F`）。

### 3. 取得 MR diff_refs
```
GET {GITLAB_API_URL}/api/v4/projects/{encoded_path}/merge_requests/{id}
```
從回傳的 `diff_refs` 中取出 `base_sha`、`start_sha`、`head_sha`，這三個 SHA 是留 inline comment 必要的座標。

### 4. 列出 review 發現，等待使用者選擇
從目前對話中整理所有 review 問題，區分為兩類：

**A. 有明確檔案路徑（+ 行號）的問題** → 留 inline comment
**B. 整體架構、無特定行號的建議** → 留 general summary comment

使用 `AskUserQuestion` 工具，以 `multiSelect: true` 呈現所有問題，讓使用者直接勾選要留言的項目：

- 每個選項的 `label` 格式：`🔴 / 🟡 / 🟢  <問題摘要>（檔案路徑[:行號]）`
- 「✅ 做得好的地方」**不列入選項**，固定加入總覽

等使用者確認選擇後，再繼續後續步驟。

### 5. 留個別留言（針對**選中**的所有問題）

**A 類（有行號）→ inline comment（帶 position）：**
```
POST {GITLAB_API_URL}/api/v4/projects/{encoded_path}/merge_requests/{id}/discussions
Content-Type: application/json
{
  "body": "<粗體標題，如 **🟡 設計問題**：>\n\n<問題說明，含建議修正方式>",
  "position": {
    "position_type": "text",
    "base_sha": "<base_sha>",
    "start_sha": "<start_sha>",
    "head_sha": "<head_sha>",
    "new_path": "<檔案路徑>",
    "new_line": <行號>
  }
}
```
- `body` 格式：粗體標題（如 `**🟡 設計問題**：`）後必須換行（`\n\n`），再另起一段寫問題說明與建議修正方式，不要讓標題和內容黏在同一行
- `new_line`：使用 review 中提到的行號（新版檔案的行號）
- 若是針對已刪除的行，改用 `old_path` 和 `old_line`
- 若 GitLab 回傳 `422`（行號不在 diff 中），改為下方 B 類方式補發，並在 body 中標注檔案路徑與行號

**B 類（無特定行號）→ general comment（不帶 position）：**
```
POST {GITLAB_API_URL}/api/v4/projects/{encoded_path}/merge_requests/{id}/discussions
Content-Type: application/json
{
  "body": "<粗體標題，如 **🔴 風險**：>\n\n<問題說明，含建議修正方式>"
}
```

### 6. 留 general summary comment（**選中**的 B 類問題 + 整體摘要）
只將使用者選中的問題依優先級分組，組成以下格式的 Markdown 留言：

```
## Code Review Summary by FET

### 🔴 Bug / 風險
- **問題描述**（`檔案路徑:行號`）
  建議修正方式

### 🟡 設計問題
- **問題描述**（`檔案路徑`）
  建議修正方式

### 🟢 建議
- **問題描述**
  建議修正方式

### ✅ 做得好的地方
- **亮點描述**

---

```

再 POST 到：
```
POST {GITLAB_API_URL}/api/v4/projects/{encoded_path}/merge_requests/{id}/notes
Content-Type: application/json
{"body": "<上述 Markdown 內容>"}
```

### 7. 回報結果
列出每則留言的結果：
- ✅ Inline comment：檔案路徑:行號 → Note ID xxx
- ✅ General comment → Note ID xxx
- ❌ 失敗的項目及錯誤訊息

若對話中沒有 review 結果，請告知使用者先執行 `/gitlab-code-review <MR_URL>`。
