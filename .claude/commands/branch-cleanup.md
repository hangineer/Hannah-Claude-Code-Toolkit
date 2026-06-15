---
description: 列出已合併或過期的本機分支並協助清理
allowed-tools: Bash(git *)
---

協助使用者清理本機 git 分支：

1. 執行 `git fetch --prune` 更新遠端分支資訊。
2. 列出已合併進目前 main 分支（依該 repo 而定為 `main` 或 `master`）的本機分支，排除目前所在分支與 main 分支本身。
3. 列出最近 30 天內沒有任何 commit 的本機分支，排除目前所在分支與 main 分支本身。
4. 將兩份清單以條列方式呈現，並標註每個分支最後一次 commit 的日期與訊息。
5. 詢問使用者要刪除哪些分支（如果有）。確認後，對已合併分支執行 `git branch -d <branch>`；對未合併分支，僅在使用者明確要求強制刪除時執行 `git branch -D <branch>`。
6. 不要主動刪除任何分支 —— 必須經使用者明確確認後才執行刪除。
