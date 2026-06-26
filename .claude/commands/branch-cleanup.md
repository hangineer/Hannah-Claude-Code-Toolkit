---
description: 列出已合併或過期的本機分支並協助清理
allowed-tools: Bash(git *), AskUserQuestion
---

協助使用者清理本機 git 分支：

1. 執行 `git fetch --prune` 更新遠端分支資訊。
2. 判斷主分支名稱（`main` 或 `master`）。
3. 收集以下三類分支（排除目前所在分支、main、master、dev）：
   - **已合併**：`git branch --merged <main>` 列出的分支，標記為可用 `-d` 刪除
   - **孤兒分支**：本機存在但 `git fetch --prune` 後遠端 tracking 已消失的分支，標記為需 `-D` 強制刪除
   - **超過 30 天無 commit**：透過 `git log -1 --format="%ci"` 判斷，標記為需 `-D` 強制刪除
4. 對每個候選分支取得最後一次 commit 日期與訊息（`git log -1 --format="%ci | %s"`）。
5. 使用 `AskUserQuestion`（`multiSelect: true`）呈現所有候選分支讓使用者勾選：
   - 每個選項的 `label` 為分支名稱
   - 每個選項的 `description` 標示分類（已合併/孤兒/逾期）、最後 commit 日期、訊息，以及刪除方式（`-d` 或 `-D`）
   - 若候選分支超過 4 個，拆成多題（每題最多 4 個選項）分批詢問
   - 若沒有任何候選分支，直接告知使用者目前沒有可清理的分支
6. 依使用者選擇執行刪除：
   - 已合併分支：`git branch -d <branch>`
   - 其餘分支：`git branch -D <branch>`
7. 不要主動刪除任何分支 —— 必須等使用者在 `AskUserQuestion` 中勾選後才執行。
