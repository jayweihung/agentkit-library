# 寫一行進度（kit note）

使用者同時開好幾個 agent，靠每個 agent 自己寫的一行進度知道它做到哪。畫面程式（例如終端機每一格的標題列）會顯示它。

- 在這些時候跑 `kit note "<剛做了什麼；下一步>"`：做完一段、確認或推翻一個猜測、卡住（等人、等權限、缺東西）、從查問題轉到修、從修轉到驗證、整件事做完。
- 寫之前先跑 `kit note`（不帶文字）看現在寫的是什麼：還有用的留下，過時的拿掉，再寫新的。
- 第一行寫動作和下一步，要具體（哪個檔案、哪個測試）；需要的話第二行寫目標。最多兩行，用使用者的語言。
- 不要每個小步驟都寫，也不要寫給自己看的流水帳。
- 剛接手一個資料夾（重開、交接）時，先跑 `kit note --history` 看之前的 agent 寫到哪。
- 停下來等使用者同意才能做下一步（例如裝東西、上線、改設定、簽章）時，先跑 `kit pending add "要你同意：<什麼>" --id <短名字>`，畫面程式會提醒使用者；使用者回了之後跑 `kit pending done <短名字>`。一般的提問、做完等使用者看，不用記。
- 在 Herdr 裡跑（有 `$HC_TERMINAL_ID`）時，同一個時機也重寫 `~/.config/herdr-app/mods/agent-page/.pages/$HC_TERMINAL_ID/status.json`（這台沒有 `mods/agent-page` 就寫 `pages/` 不加點；先 `mkdir -p`），整個檔是 `{"title","updated","waiting":[{"text","cmd"}],"doing":[{"text","project"}],"todo":[…],"done":[{"text","project","date"}]}`，做完的留著：使用者在 agent 旁的說明頁看它，不用一個一個問。
- 同一個資料夾放給使用者看的說明頁（`<時間>-<主題>.html`）時，讓它跟著 Herdr 的外觀和字型走：顏色用 `--bg --panel --fg --muted --line --accent` 這幾個名字，其他顏色的深色值寫在 `:root[data-theme="dark"]`，`<head>` 的 `<style>` 後面貼這段（agent-page 會把 Herdr 的主題放在網址 `#` 後面）：
  `<script>(function(){function a(){var p=new URLSearchParams(location.hash.slice(1)),r=document.documentElement,m=p.get("mode");if(m!=="light"&&m!=="dark")return;r.dataset.theme=m;r.style.colorScheme=m;["bg","panel","fg","muted","line","accent"].forEach(function(k){var v=p.get(k);if(/^#[0-9a-f]{3,8}$/i.test(v||""))r.style.setProperty("--"+k,v)});var c=function(k){return(p.get(k)||"").replace(/[^\p{L}\p{N} ._-]/gu,"")},f=c("font"),o=c("mono"),s=document.getElementById("herdr-font")||document.head.appendChild(Object.assign(document.createElement("style"),{id:"herdr-font"}));s.textContent=(f?'body{font-family:"'+f+'",system-ui,sans-serif!important}':"")+(o?'code,pre,kbd,samp{font-family:"'+o+'",ui-monospace,monospace!important}':"")}a();addEventListener("hashchange",a)})();</script>`
- 沒有 `kit` 指令、kit 說找不到上面的 agent、或被沙箱擋（不能寫 `~/.config/agentkit`），就略過，不用跟使用者提。
