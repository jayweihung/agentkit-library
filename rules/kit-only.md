# 裝 skill、MCP、外掛：只能透過 kit

這台的 skill、MCP、外掛由 kit 統一管。不是公司的（工具原廠、公司管理員派發的、公司專案 commit 進 git 的），又不是 kit 放的，`kit sync` 會讓 Claude Code、Codex、omp 都不載入它。

- 不要用 npx、pip、`claude plugin install`、`codex plugin add`、`omp plugin install`、`omp skill install`、`claude mcp add` 或手動複製，直接把 skill、MCP、外掛裝進 `~/.claude`、`~/.codex`、`~/.agents`、`~/.omp` 或專案的同名資料夾。裝了也會被擋下。
- 要用別人寫的：`kit collect <原作者 repo 網址> --to <自己的來源> [--allow]`，再 `kit add skill|plugin <名字>`；MCP 用 `kit new mcp --config`。不確定收進哪個來源，先問使用者。
- 要用自己寫的：`kit new skill <名字> --from <本機資料夾>`。
- 安裝說明要你跑某個安裝程式時，先停下來，改用上面的 kit 指令，並告訴使用者為什麼。
- 被擋下的東西在 `kit list --json` 的 `blocked`，或 Herdr 的 Kit 面板。

## 改了 kit 的來源，就要送出

- 改了 kit 來源 repo 裡的東西（規則、技能、MCP、外掛、agent 定義；`kit list --json` 的 `sources` 列出這些 repo 在哪），做完就跑 `kit push --to <來源>`，其他機器同步時才拿得到。只改了自己這台的話，各機器的規則會不一樣。
- `kit push` 被 `kit check` 擋下（例如私人字眼）：照它說的改，再送一次；不要繞過。
- 送出後告訴使用者送到哪個來源、是直接推還是開了 PR。
