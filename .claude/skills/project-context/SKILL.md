---
name: project-context
description: 當使用者要求「介紹這個專案」、「這個專案是做什麼的」、「幫我了解這個 repo」，或在新對話開始時需要快速了解專案結構、技術棧與慣例時使用。
version: 0.1.0
---

# Project Context

## 目標

快速整理專案的結構、技術棧與開發慣例，協助使用者（或新加入的協作者）盡快上手這個專案。

## 步驟

1. **基本資訊**：閱讀 `README.md` 與 `CLAUDE.md`，了解專案目的與現有文件。
2. **技術棧**：檢查相依套件設定檔（例如 `package.json`、`pyproject.toml`、`go.mod`、`Cargo.toml` 等），列出主要語言、框架與關鍵相依套件。
3. **目錄結構**：列出專案主要目錄（約 2-3 層，排除 `.git`、`node_modules`、`dist`、`build` 等），並簡述每個目錄的用途。
4. **開發慣例**：
   - 檢查 lint/format 設定（例如 `.eslintrc`、`.prettierrc`、`pyproject.toml` 中的 `[tool.ruff]` 等）
   - 檢查測試框架與測試目錄位置
   - 檢查 `.claude/` 中的自訂 command、agent、skill，並簡述其用途
5. **近期動態**：執行 `git log --oneline -10` 了解近期變更方向。

## 輸出格式

以條列方式呈現摘要，結構如下：

- **專案概覽**：一到兩句話描述這個專案是什麼
- **技術棧**：語言、框架、關鍵相依套件
- **目錄結構**：主要目錄與其用途
- **開發慣例**：lint/format/測試慣例、Claude 工具箱內容
- **近期動態**：近期 commit 的方向

摘要應簡潔，避免逐行列出檔案內容；若使用者之後想深入了解特定部分，再參考對應檔案即可。
