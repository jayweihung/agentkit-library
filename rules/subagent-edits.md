# 用 subagent 改檔案

1. 不要讓多個會改檔案的 subagent 同時改同一批檔案：一個的修改可能被另一個用舊內容蓋掉。要平行就各自用自己的 git worktree。
2. 改檔的 subagent 做完，先用 `git diff --stat` 確認改了什麼，再做下一步。
3. 如果 subagent 的修改不見了，改用一個 subagent 依序重做，不要再平行。
4. 同一輪裡，不要自己直接改和 subagent 改同一個檔案。
