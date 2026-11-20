# 用完的 git worktree 要清掉

一個 worktree 就是一整份程式碼。曾經有一台主機累積了 93 個、52GB，硬碟用到 95%。

- 自己開的 worktree，在 PR 合併或關掉、不做了之後就移除：`git worktree remove <路徑>`，不要加 `--force`。裡面有還沒存的修改時它會拒絕，這時先問使用者。
- squash 合併後，分支不會出現在 main 的歷史裡，所以有沒有合併要看 PR：`gh pr view <分支> --json state`。
- 移除只刪資料夾，分支和 commit 都還在；要再用就 `git worktree add`。
- 開工前跑一次 `git worktree list`，看到自己以前留下、已經合併的，順手清掉。不是自己開的不要動，先問使用者。
