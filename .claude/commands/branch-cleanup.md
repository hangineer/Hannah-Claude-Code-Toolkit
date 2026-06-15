---
description: List merged or stale local branches and help clean them up
allowed-tools: Bash(git *)
---

Help the user clean up local git branches:

1. Run `git fetch --prune` to update remote branch information.
2. List local branches that have already been merged into the current main branch (`main` or `master`, depending on the repo), excluding the current branch and the main branch itself.
3. List local branches with no commits in the last 30 days, excluding the current branch and the main branch itself.
4. Present both lists as bullet points, noting each branch's last commit date and message.
5. Ask the user which branches (if any) they want to delete. If confirmed, run `git branch -d <branch>` (for merged branches) or `git branch -D <branch>` (for unmerged branches, only if the user explicitly requests a force delete).
6. Do not delete any branch proactively — only delete after explicit user confirmation.
