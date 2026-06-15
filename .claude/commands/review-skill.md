---
description: 呼叫 skill-reviewer subagent，檢查新增/修改的 command、agent 或 skill 是否符合 CLAUDE.md 的慣例
argument-hint: "[要檢查的檔案路徑，預設為目前對話中新增/修改的 command、agent、skill]"
---

請使用 `skill-reviewer` subagent，檢查使用者指定（或目前對話中新增/修改）的 command、agent、skill 檔案是否符合 `CLAUDE.md` 中的命名與 frontmatter 慣例。

1. 若使用者在指令參數中指定了檔案路徑，將其交給 `skill-reviewer` 檢查；否則由 `skill-reviewer` 自行找出目前對話或目前 git 變更中新增/修改的 `.claude/commands/`、`.claude/agents/`、`.claude/skills/` 檔案。
2. 將 `skill-reviewer` 回報的 checklist（pass/fail 與建議修正）原樣呈現給使用者。
3. 不要自行修改檔案 —— 修正交由使用者決定後再進行。
