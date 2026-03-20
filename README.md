# 45 個 Claude Code 技巧：從入門到進階

這裡是我整理的 Claude Code 使用技巧，包括自訂狀態列腳本、把 system prompt 砍掉一半、用 Gemini CLI 當 Claude Code 的小弟、以及讓 Claude Code 在容器裡跑自己。另外還有 [dx plugin](#tip-44-安裝-dx-plugin)。

📺 [快速 demo](https://www.youtube.com/watch?v=hiISl558JGE) - 看看其中一些技巧的實際操作，包括多個 Claude 的工作流程和語音輸入：

[![Demo video thumbnail](assets/demo-thumbnail.png)](https://www.youtube.com/watch?v=hiISl558JGE)

<!-- TOC -->
## 目錄

- [Tip 0: 自訂你的狀態列](#tip-0-自訂你的狀態列)
- [Tip 1: 學幾個必備的 slash command](#tip-1-學幾個必備的-slash-command)
- [Tip 2: 用語音跟 Claude Code 對話](#tip-2-用語音跟-claude-code-對話)
- [Tip 3: 把大問題拆成小問題](#tip-3-把大問題拆成小問題)
- [Tip 4: 像高手一樣用 Git 和 GitHub CLI](#tip-4-像高手一樣用-git-和-github-cli)
- [Tip 5: AI context 就像牛奶，越新鮮越濃縮越好！](#tip-5-ai-context-就像牛奶越新鮮越濃縮越好)
- [Tip 6: 從終端機把輸出拿出來](#tip-6-從終端機把輸出拿出來)
- [Tip 7: 設定終端機 alias 快速啟動](#tip-7-設定終端機-alias-快速啟動)
- [Tip 8: 主動壓縮你的 context](#tip-8-主動壓縮你的-context)
- [Tip 9: 完成「寫 → 測試」循環來跑自動化任務](#tip-9-完成寫--測試循環來跑自動化任務)
- [Tip 10: Cmd+A 和 Ctrl+A 是你的好朋友](#tip-10-cmda-和-ctrla-是你的好朋友)
- [Tip 11: 用 Gemini CLI 作為被封鎖網站的備案](#tip-11-用-gemini-cli-作為被封鎖網站的備案)
- [Tip 12: 投資你自己的工作流程](#tip-12-投資你自己的工作流程)
- [Tip 13: 搜尋你的對話紀錄](#tip-13-搜尋你的對話紀錄)
- [Tip 14: 用終端機分頁做多工](#tip-14-用終端機分頁做多工)
- [Tip 15: 精簡 system prompt](#tip-15-精簡-system-prompt)
- [Tip 16: 用 Git worktree 平行處理分支](#tip-16-用-git-worktree-平行處理分支)
- [Tip 17: 手動指數退避處理長時間任務](#tip-17-手動指數退避處理長時間任務)
- [Tip 18: 把 Claude Code 當寫作助手](#tip-18-把-claude-code-當寫作助手)
- [Tip 19: Markdown 超讚](#tip-19-markdown-超讚)
- [Tip 20: 用 Notion 保留貼上時的連結](#tip-20-用-notion-保留貼上時的連結)
- [Tip 21: 用容器跑長時間的高風險任務](#tip-21-用容器跑長時間的高風險任務)
- [Tip 22: 學好 Claude Code 最好的方法就是一直用它](#tip-22-學好-claude-code-最好的方法就是一直用它)
- [Tip 23: Clone/fork 和 half-clone 對話](#tip-23-clonefork-和-half-clone-對話)
- [Tip 24: 用 realpath 取得絕對路徑](#tip-24-用-realpath-取得絕對路徑)
- [Tip 25: 搞懂 CLAUDE.md、Skills、Slash Commands 和 Plugins 的差別](#tip-25-搞懂-claudemdskillsslash-commands-和-plugins-的差別)
- [Tip 26: 互動式 PR review](#tip-26-互動式-pr-review)
- [Tip 27: 把 Claude Code 當研究工具](#tip-27-把-claude-code-當研究工具)
- [Tip 28: 精通各種驗證輸出的方法](#tip-28-精通各種驗證輸出的方法)
- [Tip 29: 把 Claude Code 當 DevOps 工程師](#tip-29-把-claude-code-當-devops-工程師)
- [Tip 30: 保持 CLAUDE.md 簡潔並定期檢視](#tip-30-保持-claudemd-簡潔並定期檢視)
- [Tip 31: Claude Code 作為萬用介面](#tip-31-claude-code-作為萬用介面)
- [Tip 32: 關鍵在於選擇對的抽象層級](#tip-32-關鍵在於選擇對的抽象層級)
- [Tip 33: 審查你已批准的指令](#tip-33-審查你已批准的指令)
- [Tip 34: 多寫測試（用 TDD）](#tip-34-多寫測試用-tdd)
- [Tip 35: 在未知領域更勇敢一點；迭代式解決問題](#tip-35-在未知領域更勇敢一點迭代式解決問題)
- [Tip 36: 在背景執行 bash 指令和 subagent](#tip-36-在背景執行-bash-指令和-subagent)
- [Tip 37: 個人化軟體的時代來了](#tip-37-個人化軟體的時代來了)
- [Tip 38: 在輸入框裡移動和編輯](#tip-38-在輸入框裡移動和編輯)
- [Tip 39: 花點時間規劃，但也要快速做原型](#tip-39-花點時間規劃但也要快速做原型)
- [Tip 40: 簡化過度複雜的程式碼](#tip-40-簡化過度複雜的程式碼)
- [Tip 41: 自動化的自動化](#tip-41-自動化的自動化)
- [Tip 42: 分享你的知識，能貢獻就貢獻](#tip-42-分享你的知識能貢獻就貢獻)
- [Tip 43: 持續學習！](#tip-43-持續學習)
- [Tip 44: 安裝 dx plugin](#tip-44-安裝-dx-plugin)
- [Tip 45: 快速設定腳本](#tip-45-快速設定腳本)

<!-- /TOC -->

## Tip 0: 自訂你的狀態列

你可以自訂 Claude Code 底部的狀態列來顯示有用的資訊。我的設定會顯示模型、目前目錄、git branch（如果有的話）、未提交的檔案數量、跟 origin 的同步狀態，以及 token 用量的進度條。它還會顯示第二行，放我最後一則訊息，這樣我可以看到這段對話是在做什麼：

```
Opus 4.5 | 📁claude-code-tips | 🔀main (scripts/context-bar.sh uncommitted, synced 12m ago) | ██░░░░░░░░ 18% of 200k tokens
💬 This is good. I don't think we need to change the documentation as long as we don't say that the default color is orange el...
```

這對於隨時注意 context 用量和記住你在做什麼特別有幫助。這個腳本還支援 10 種配色主題（orange、blue、teal、green、lavender、rose、gold、slate、cyan 或 gray）。

![Color preview options](scripts/color-preview.png)

設定方式可以用[這個範例腳本](scripts/context-bar.sh)，並參考[設定說明](scripts/README.md)。

## Tip 1: 學幾個必備的 slash command

有不少內建的 slash command（打 `/` 就能看到全部）。這裡列幾個值得知道的：

### /usage

查看你的速率限制：

```
 Current session
 █████████▌                                         19% used
 Resets 12:59am (America/Vancouver)

 Current week (all models)
 █████████████████████▌                             43% used
 Resets Feb 3 at 1:59pm (America/Vancouver)

 Current week (Sonnet only)
 ███████████████████▌                               39% used
 Resets 8:59am (America/Vancouver)
```

如果你想密切關注用量，可以在一個分頁裡開著它，然後用 Tab 再 Shift+Tab 或 ← 再 → 來重新整理。

### /chrome

切換 Claude 的原生瀏覽器整合：

```
> /chrome
Chrome integration enabled
```

### /mcp

管理 MCP（Model Context Protocol）server：

```
 Manage MCP servers
 1 server

 ❯ 1. playwright  ✔ connected · Enter to view details

 MCP Config locations (by scope):
  • User config (available in all your projects):
    • /Users/yk/.claude.json
```

### /stats

用 GitHub 風格的活動圖表查看你的使用統計：

```
      Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec Jan
      ··········································▒█░▓░█░▓▒▒
  Mon ·········································▒▒██▓░█▓█░█
      ·········································░▒█▒▓░█▒█▒█
  Wed ········································░▓▒█▓▓░▒▓▒██
      ········································░▓░█▓▓▓▓█░▒█
  Fri ········································▒░░▓▒▒█▓▓▓█
      ········································▒▒░▓░░▓▒▒░░

      Less ░ ▒ ▓ █ More

  Favorite model: Opus 4.5        Total tokens: 17.6m

  Sessions: 4.1k                  Longest session: 20h 40m 45s
  Active days: 79/80              Longest streak: 75 days
  Most active day: Jan 26         Current streak: 74 days

  You've used ~24x more tokens than War and Peace
```

### /clear

清除對話，重新開始。

## Tip 2: 用語音跟 Claude Code 對話

我發現用語音溝通比用手打字快很多。在本機上用語音轉文字系統來輔助真的很有幫助。

在我的 Mac 上，我試過幾個不同的選項：
- [superwhisper](https://superwhisper.com/)
- [MacWhisper](https://goodsnooze.gumroad.com/l/macwhisper)
- [Super Voice Assistant](https://github.com/ykdojo/super-voice-assistant)（開源，支援 Parakeet v2/v3）

你用雲端服務可以得到更高的準確度，但我發現本機模型對這個用途來說已經夠強了。就算轉錄有錯字或誤聽，Claude 聰明到能理解你想說什麼。有時候某些詞需要講特別清楚，但整體來說本機模型表現得夠好。

舉個例子，在這個截圖中你可以看到 Claude 能正確理解被誤轉錄的詞，像是「ExcelElanishMark」和「advast」被正確解讀為「exclamation mark」和「Advanced」：

![Voice transcription mistakes interpreted correctly](assets/voice-transcription-mistakes.png)

我覺得最好的思考方式是，想像你在跟朋友溝通。當然，你可以透過文字溝通，對某些人來說可能比較容易，或者用 email，這完全沒問題。大多數人似乎都是這樣用 Claude Code 的。但如果你想溝通得更快，何不打個快速電話？你可以只是發語音訊息。你不需要真的跟 Claude Code 打電話，就是發一堆語音訊息就好。至少對我這個練了好幾年說話藝術的人來說更快。但我覺得對大多數人來說也會更快。

常見的反對意見是「如果跟其他人在同一個房間呢？」我就用耳機小聲講——我個人喜歡用 Apple EarPods（不是 AirPods）。它們價格實惠、品質夠好，你只要小聲對著它講就行了。我在其他人面前做過，效果很好。辦公室裡本來就有人在講話——你只是改成安靜地對你的語音轉錄系統講話而已。我覺得完全沒問題。這個方法好到連在飛機上都能用。夠大聲讓別人聽不到你，但如果你離麥克風夠近，你的本機模型還是能聽懂你在說什麼。（事實上，我就是在一趟飛行中用這個方法寫的這段話。）

**更新：** Claude Code 現在有[內建的語音模式](https://x.com/bcherny/status/2032238378389840018)了。我測試過覺得不錯，但我個人還是用本機模型，因為我覺得比較快。

## Tip 3: 把大問題拆成小問題

這是最重要的概念之一。這跟傳統軟體工程完全一樣——最好的軟體工程師早就知道怎麼做了，而且同樣適用於 Claude Code。

如果你發現 Claude Code 沒辦法一次解決一個困難的問題或程式任務，叫它把問題拆成多個小問題。看看它能不能解決問題的其中一個部分。如果還是太難，看看它能不能解決更小的子問題。一直拆到全部都能解決為止。

基本上，與其從 A 直接到 B：

![Direct approach](assets/breakdown-direct.png)

你可以從 A 到 A1 到 A2 到 A3，然後到 B：

![Step-by-step approach](assets/breakdown-steps.png)

一個好的例子是我在做自己的語音轉錄系統的時候。我需要做一個系統，讓使用者可以選擇和下載模型、接收鍵盤快捷鍵、開始轉錄、把轉錄的文字放到使用者的游標位置，然後把這些全部包在一個好看的 UI 裡。這東西很多。所以我把它拆成小任務。首先，我做了一個只會下載模型的執行檔，什麼別的都不做。然後做了一個只會錄音的。再做一個只會轉錄預錄音檔的。我就這樣一個一個完成，最後再把它們組合起來。

跟這高度相關的是：你的問題解決能力和軟體工程技能在 agentic coding 和 Claude Code 的世界裡仍然非常重要。它能自己解決很多問題，但當你把你的通用問題解決和軟體工程技能應用在上面時，它會變得強大很多。

## Tip 4: 像高手一樣用 Git 和 GitHub CLI

直接叫 Claude 處理你的 Git 和 GitHub CLI 任務就好。包括 commit（這樣你就不用自己寫 commit message）、branching、pulling 和 pushing。

我個人讓 pull 自動批准但 push 不會，因為 push 比較危險——如果 pull 出了什麼問題，它不會污染 origin。

GitHub CLI（`gh`）可以做的事情很多。我開始用 Claude Code 後做得更多的一件事是建立 draft PR。這讓 Claude Code 用低風險的方式處理 PR 建立流程——你可以在標記為 ready for review 之前檢視所有內容。

而且 `gh` 其實很強大。你甚至可以透過它送任意的 GraphQL 查詢。舉例來說，你甚至可以找到 GitHub PR description 被編輯的確切時間：

```
⏺ Bash(gh api graphql -f query='
      query {
        repository(owner: "...", name: "...") {
          pullRequest(number: ...) {
            userContentEdits(first: 100) {
              nodes { editedAt editor { login } }
            }
          }
        }
      }')

⏺ Here's the full edit history for your PR description:

  | #  | Edited At (UTC)     | Editor |
  |----|---------------------|--------|
  | 1  | 2025-12-01 00:08:34 | ykdojo |
  | 2  | 2025-12-01 15:57:21 | ykdojo |
  | 3  | 2025-12-01 16:24:33 | ykdojo |
  | 4  | 2025-12-01 16:27:00 | ykdojo |
  | 5  | 2025-12-04 00:40:02 | ykdojo |
  ...
```

### 停用 commit/PR 署名

預設情況下，Claude Code 會在 commit 加上 `Co-Authored-By` 尾標，在 PR 加上署名頁尾。你可以在 `~/.claude/settings.json` 加入以下設定來停用：

```json
{
  "attribution": {
    "commit": "",
    "pr": ""
  }
}
```

把兩個都設成空字串就會完全移除署名。這取代了舊的 `includeCoAuthoredBy` 設定，那個已經棄用了。

## Tip 5: AI context 就像牛奶，越新鮮越濃縮越好！

當你跟 Claude Code 開一段新對話時，它的表現最好，因為它不需要處理之前對話累積的複雜 context。但隨著你跟它聊越久，context 越長，表現通常會下降。

所以最好每個新主題都開一段新對話，或者當表現開始下降時就重新開始。

## Tip 6: 從終端機把輸出拿出來

有時候你想複製 Claude Code 的輸出，但直接從終端機複製不一定很乾淨。以下是幾種更容易把內容拿出來的方法：

- **`/copy` 指令**：最簡單的方法——打 `/copy` 就能把 Claude 的最後一個回覆以 markdown 格式複製到剪貼簿
- **直接用剪貼簿**：在 Mac 或 Linux 上，叫 Claude 用 `pbcopy` 把輸出直接送到你的剪貼簿
- **寫到檔案**：讓 Claude 把內容放到一個檔案裡，然後叫它用 VS Code（或你喜歡的編輯器）打開，這樣你就能從那裡複製。你也可以指定行號，這樣可以叫 Claude 打開它剛編輯的那一行。如果是 markdown 檔案，在 VS Code 裡打開後，你可以用 Cmd+Shift+P（Linux/Windows 用 Ctrl+Shift+P）然後選「Markdown: Open Preview」來看渲染後的版本
- **開啟 URL**：如果有個 URL 你想自己看，叫 Claude 用瀏覽器打開它。Mac 上可以叫它用 `open` 指令，但一般來說叫它用你喜歡的瀏覽器打開，在任何平台都能用
- **GitHub Desktop**：你可以叫 Claude 用 GitHub Desktop 打開目前的 repo。當它在非根目錄下工作時特別有用——例如你叫它在不同目錄建了一個 git worktree，而你還沒從那裡打開 Claude Code

這些方法也可以組合使用。例如，如果你想編輯一個 GitHub PR description，與其讓 Claude 直接編輯（它可能搞砸），你可以先讓它把內容複製到本機檔案。讓它編輯那個檔案，你自己檢查結果，看起來沒問題後，再讓它複製貼回 GitHub PR。這樣做效果很好。或者如果你想自己來，可以叫它用 VS Code 打開或透過 pbcopy 給你，讓你自己手動複製貼上。

當然，這些指令你自己也能跑，但如果你發現自己重複在做，讓 Claude 幫你跑會更方便。

## Tip 7: 設定終端機 alias 快速啟動

因為 Claude Code 的關係我更常用終端機了，所以我發現設定簡短的 alias 來快速啟動東西很有幫助。以下是我用的：

- `c` 代表 Claude Code（這是我最常用的）
- `ch` 代表 Claude Code 加上 Chrome 整合
- `gb` 代表 GitHub Desktop
- `co` 代表 VS Code
- `q` 代表跳到我放大部分專案的目錄。從那裡我可以手動 cd 進某個資料夾來做那個專案，或者直接用 `c` 啟動 Claude Code，讓它基本上可以存取任何它需要的專案。

設定方式是在你的 shell 設定檔（`~/.zshrc` 或 `~/.bashrc`）加入這樣的行：

```bash
alias c='claude'
alias ch='claude --chrome'
alias gb='github'
alias co='code'
alias q='cd ~/Desktop/projects'
```

有了這些 alias 後，你可以搭配旗標使用：`c -c` 繼續你上次的對話，`c -r` 顯示最近的對話列表讓你選擇恢復。這些在 `ch` 上也能用（`ch -c`、`ch -r`）來恢復 Chrome 會話。

## Tip 8: 主動壓縮你的 context

Claude Code 有個 `/compact` 指令可以摘要你的對話來釋放 context 空間。當完整的可用 context 被填滿時，自動壓縮也會觸發。Opus 4.5 目前的可用 context window 總共是 200k，其中 45k 保留給自動壓縮。總共 200k 的大約 10% 會自動被 system prompt、工具、memory 和動態 context 佔掉。但我發現主動做壓縮並手動調整會更好。我用 `/config` 關掉了 auto-compact，這樣主要對話有更多 context 可用，而且我能更好地控制壓縮的時機和方式。

我的做法是在開始新對話前叫 Claude 寫一份 handoff 文件。像這樣：

> 把剩下的計畫放在 system-prompt-extraction 資料夾裡的 HANDOFF.md。說明你試過什麼、什麼有效、什麼沒效，這樣下一個有新鮮 context 的 agent 只要載入那個檔案就能開始接手完成這個任務。

Claude 會建立一個摘要目前工作狀態的檔案：

```
⏺ Write(experiments/system-prompt-extraction/HANDOFF.md)
  ⎿  Wrote 129 lines to experiments/system-prompt-extraction/HANDOFF.md
     # System Prompt Slimming - Handoff Document
     ## Goal
     Reduce Claude Code's system prompt by ~45% (currently at 11%, need ~34% more).
     ## Current Progress
     ### What's Been Done
     - **Backup/restore system**: `backup-cli.sh` and `restore-cli.sh` with SHA256 verification
     - **Patch system**: `patch-cli.js` that restores from backup then applies patches
     ...
```

Claude 寫完後，快速看一下。如果有什麼遺漏，要求修改：

> 你有加上關於要迭代測試而不是一次做完所有事情的備註嗎？

然後開一段新對話。對新的 agent 來說，你只要給檔案路徑就好，什麼都不用多說，它應該就能正常運作：

```
> experiments/system-prompt-extraction/HANDOFF.md
```

在後續的對話中，你可以叫 agent 為下一個 agent 更新這份文件。

我還做了一個 `/handoff` slash command 來自動化這個流程——它會檢查現有的 HANDOFF.md，如果存在就讀取它，然後建立或更新，包含目標、進度、什麼有效、什麼沒效、和下一步。你可以在 [skills 資料夾](skills/handoff/SKILL.md) 找到它，或透過 [dx plugin](#tip-44-安裝-dx-plugin) 安裝。

**替代方案：用 plan mode**

另一個選項是用 plan mode。用 `/plan` 或 Shift+Tab 進入。叫 Claude 收集所有相關的 context 並為下一個 agent 建立一個完整的計畫：

> 我剛啟用了 plan mode。把下一個 agent 需要的所有 context 都帶過來。下一個 agent 不會有任何其他 context，所以你需要夠完整。

Claude 會探索 codebase、收集 context，然後寫一個詳細的計畫。完成後，你會看到這樣的選項：

```
Would you like to proceed?

❯ 1. Yes, clear context and auto-accept edits (shift+tab)
  2. Yes, auto-accept edits
  3. Yes, manually approve edits
  4. Type here to tell Claude what to change
```

選項 1 會清除先前的 context 並用這個計畫重新開始。新的 Claude instance 只看到計畫，所以它可以專注在任務上，不用背負舊對話的包袱。它也會拿到舊的 transcript 檔案連結，以便需要時查看特定細節。

## Tip 9: 完成「寫 → 測試」循環來跑自動化任務

如果你要讓 Claude Code 自動跑某個東西，像是 `git bisect`，你需要給它一個驗證結果的方式。關鍵是完成「寫 → 測試」循環：寫程式碼、跑它、檢查輸出、重複。

舉個例子，假設你在開發 Claude Code 本身，然後你發現 `/compact` 壞了，開始丟 400 錯誤。一個經典的工具來找出造成這個問題的確切 commit 是 `git bisect`。好處是你可以讓 Claude Code 對自己跑 bisect，但它需要一個方式來測試每個 commit。

對於涉及互動式終端機的任務（像 Claude Code 本身），你可以用 tmux。模式是這樣的：

1. 啟動一個 tmux session
2. 發送指令到裡面
3. 擷取輸出
4. 驗證它是你期望的

這是一個測試 `/context` 是否正常運作的簡單範例：

```bash
tmux kill-session -t test-session 2>/dev/null
tmux new-session -d -s test-session
tmux send-keys -t test-session 'claude' Enter
sleep 2
tmux send-keys -t test-session '/context' Enter
sleep 1
tmux capture-pane -t test-session -p
```

一旦你有了這樣的測試，Claude Code 就可以跑 `git bisect` 並自動測試每個 commit，直到找到那個搞壞東西的 commit。

這也是一個為什麼你的軟體工程技能仍然重要的例子。如果你是軟體工程師，你可能知道像 `git bisect` 這樣的工具。這些知識在跟 AI 合作時仍然非常有價值——你只是用不同的方式來應用它。

另一個例子就是寫測試。讓 Claude Code 寫完一些程式碼後，如果你想測試它，可以讓它也幫自己寫測試。讓它自己跑並修復問題。當然，它不一定總是往對的方向走，有時你需要監督，但它能自己完成的程式任務多到令人驚訝。

### 創意測試策略

有時候你需要發揮創意來完成「寫 → 測試」循環。例如，如果你在做一個 web app，你可以用 Playwright MCP、Chrome DevTools MCP，或 Claude 的原生瀏覽器整合（透過 `/chrome`）。我還沒試過 Chrome DevTools，但我試過 Playwright 和 Claude 的原生整合。整體來說，Playwright 通常表現比較好。它確實會用不少 context，但 200k 的 context window 通常夠一個任務或幾個小任務使用。

這兩者的主要差別似乎在於 Playwright 著重於 accessibility tree（頁面元素的結構化資料）而不是截圖。它有截圖的能力，但通常不用截圖來執行動作。另一方面，Claude 的原生瀏覽器整合更著重於截圖和用特定座標點擊元素。它有時會點到奇怪的地方，整個過程可能比較慢。

這可能會隨時間改善，但預設我會對大多數非視覺密集的任務選擇 Playwright。我只在需要使用已登入的狀態（不用提供帳密，因為它跑在你自己的瀏覽器 profile）時，或者特別需要用座標視覺點擊元素時，才會用 Claude 的原生瀏覽器整合。

這就是為什麼我預設停用 Claude 的原生瀏覽器整合，只透過之前定義的 `ch` 快捷鍵使用。這樣 Playwright 處理大部分瀏覽器任務，我只在特別需要時才啟用 Claude 的原生整合。

另外，你可以叫它用 accessibility tree ref 而不是座標。以下是我在 CLAUDE.md 裡寫的：

```markdown
# Claude for Chrome

- Use `read_page` to get element refs from the accessibility tree
- Use `find` to locate elements by description
- Click/interact using `ref`, not coordinates
- NEVER take screenshots unless explicitly requested by the user
```

在我的個人經驗中，我還遇過一個情況：我在做一個 Python 函式庫（[Daft](https://github.com/Eventual-Inc/Daft)），需要在 Google Colab 上測試我在本機建置的版本。問題是在 Google Colab 上建置一個有 Rust 後端的 Python 函式庫很困難——似乎不太行。所以我需要在本機建置一個 wheel 然後手動上傳，才能在 Google Colab 上跑。我也試過 monkey patching，在我等完整 wheel 在本機建置之前的短期內效果不錯。這些測試策略都是我跟 Claude Code 來回討論後想出來的。

我遇到的另一個情況是需要在 Windows 上測試，但我沒有 Windows 機器。同個 repo 上的 CI 測試失敗了，因為我們的 Rust 在 Windows 上有一些問題，而我沒辦法在本機測試。所以我需要建一個包含所有改動的 draft PR，另一個包含同樣改動加上在非 main branch 啟用 Windows CI 跑測試的 draft PR。我指示 Claude Code 做了所有這些事，然後直接在新 branch 上測試 CI。

## Tip 10: Cmd+A 和 Ctrl+A 是你的好朋友

我已經講了好幾年了：在 AI 的世界裡 Cmd+A 和 Ctrl+A 是好朋友。這同樣適用於 Claude Code。

有時候你想給 Claude Code 一個 URL，但它無法直接存取。可能是私密頁面（不是敏感資料，只是非公開的），或是像 Reddit 這種 Claude Code 抓不到的東西。這時候，你可以直接全選你看到的內容（Mac 用 Cmd+A，其他平台用 Ctrl+A），複製，然後直接貼到 Claude Code。這是一個很強大的方法。

這對終端機輸出也很好用。當我有 Claude Code 本身或任何其他 CLI 應用的輸出時，可以用同樣的技巧：全選、複製、貼回 CC。很有幫助。

有些頁面預設不太適合全選——但有技巧可以先把它們轉成更好的狀態。例如 Gmail 信件串，點「全部列印」取得列印預覽（但取消實際列印）。那個頁面會把信件串裡的所有郵件展開，所以你可以乾淨地 Cmd+A 整個對話。

這適用於任何 AI，不只是 Claude Code。

## Tip 11: 用 Gemini CLI 作為被封鎖網站的備案

Claude Code 的 WebFetch 工具無法存取某些網站，像是 Reddit。但你可以透過建立一個 skill 來解決這個問題，告訴 Claude 用 Gemini CLI 作為備案。Gemini 有網路存取能力，可以從 Claude 直接抓不到的網站取得內容。

這用了跟 Tip 9 一樣的 tmux 模式——啟動一個 session、發送指令、擷取輸出。Skill 檔案放在 `~/.claude/skills/reddit-fetch/SKILL.md`。完整內容請看 [skills/reddit-fetch/SKILL.md](skills/reddit-fetch/SKILL.md)。

Skill 更省 token，因為 Claude Code 只在需要時才載入它們。如果你想要更簡單的做法，可以把精簡版放在 `~/.claude/CLAUDE.md` 裡，但那樣不管你需不需要都會在每段對話載入。

我測試了一下，叫 Claude Code 去看 Reddit 上大家怎麼看 Claude Code skill——有點 meta。它跟 Gemini 來回了一陣子，所以不快，但報告的品質出乎意料地好。顯然，你需要先安裝 Gemini CLI 才能用。你也可以透過 [dx plugin](#tip-44-安裝-dx-plugin) 安裝這個 skill。

## Tip 12: 投資你自己的工作流程

就我個人而言，我用 Swift 從零開始做了自己的語音轉錄 app。我用 Claude Code 從零開始做了自訂狀態列，這個是用 bash。我還做了自己的系統來簡化 Claude Code 壓縮過的 JavaScript 檔案裡的 system prompt。

但你不用像我這樣搞得那麼極端。光是好好維護你自己的 CLAUDE.md，確保它盡可能精簡又能幫你達成目標——這類事情就很有幫助。當然，學這些技巧、學這些工具、還有一些最重要的功能也是。

這些都是對你用來做各種東西的工具的投資。我覺得至少花一點時間在這上面是重要的。

## Tip 13: 搜尋你的對話紀錄

你可以問 Claude Code 關於你過去的對話，它會幫你找到和搜尋它們。你的對話紀錄儲存在本機的 `~/.claude/projects/` 裡，資料夾名稱是基於專案路徑（斜線變成減號）。

例如，一個在 `/Users/yk/Desktop/projects/claude-code-tips` 的專案的對話會存在：

```
~/.claude/projects/-Users-yk-Desktop-projects-claude-code-tips/
```

每段對話是一個 `.jsonl` 檔案。你可以用基本的 bash 指令搜尋：

```bash
# Find all conversations mentioning "Reddit"
grep -l -i "reddit" ~/.claude/projects/-Users-yk-Desktop-projects-*/*.jsonl

# Find today's conversations about a topic
find ~/.claude/projects/-Users-yk-Desktop-projects-*/*.jsonl -mtime 0 -exec grep -l -i "keyword" {} \;

# Extract just the user messages from a conversation (requires jq)
cat ~/.claude/projects/.../conversation-id.jsonl | jq -r 'select(.type=="user") | .message.content'
```

或者直接問 Claude Code：「我們今天有聊過關於 X 的什麼嗎？」它就會幫你搜尋紀錄。

## Tip 14: 用終端機分頁做多工

同時跑多個 Claude Code instance 時，保持組織性比任何特定的技術設定（像是 Git worktree）都重要。我建議同時最多處理三到四個任務。

我個人的方法是我稱之為「瀑布式」的做法——每當我開始一個新任務，就在右邊開一個新分頁。然後我從左掃到右、從左掃到右，從最舊的任務到最新的。整體方向保持一致，除了我需要檢查某些任務、收到通知等等的時候。

以下是我的設定通常看起來的樣子：

![Terminal tabs showing multitasking workflow](assets/multitasking-terminal-tabs.png)

在這個例子中：
1. **最左邊的分頁** - 一直跑著我的語音轉錄系統的常駐分頁（一直待在這裡）
2. **第二個分頁** - 設定 Docker 容器
3. **第三個分頁** - 檢查我本機的磁碟使用量
4. **第四個分頁** - 做一個工程專案
5. **第五個分頁（目前的）** - 正在寫這個技巧

## Tip 15: 精簡 system prompt

Claude Code 的 system prompt 和 tool definition 在你開始工作之前就佔了大約 19k token（你 200k context 的約 10%）。我做了一個 patch 系統可以把它減到大約 9k token——省下大約 10,000 token（約 50% 的開銷）。

| 元件 | 修改前 | 修改後 | 節省 |
|-----------|--------|-------|---------|
| System prompt | 3.0k | 1.8k | 1,200 tokens |
| System tools | 15.6k | 7.4k | 8,200 tokens |
| **總計** | **~19k** | **~9k** | **~10k tokens (~50%)** |

以下是 `/context` 在 patch 前後的樣子：

**未 patch（~20k，10%）**

![Unpatched context](assets/context-unpatched.png)

**已 patch（~10k，5%）**

![Patched context](assets/context-patched.png)

這些 patch 的原理是從壓縮過的 CLI bundle 中刪除冗長的範例和重複的文字，同時保留所有必要的指令。

我已經廣泛測試過，效果很好。感覺更原始——更強大，但可能規範少一點，這很合理因為 system instruction 更短了。用這種方式使用時感覺更像一個專業工具。我真的很享受從較低的 context 開始，因為你在填滿之前有更多空間，這讓你可以選擇把對話繼續得更長。這絕對是這個策略最棒的部分。

詳情請看 [system-prompt 資料夾](system-prompt/)，裡面有 patch 腳本和完整的精簡內容說明。

**為什麼用 patch？** Claude Code 有旗標可以讓你從檔案提供簡化的 system prompt（`--system-prompt` 或 `--system-prompt-file`），所以那是另一個方法。但對於 tool description，沒有官方的自訂選項。Patch CLI bundle 是唯一的方法。因為我的 patch 系統用一個統一的方式處理所有東西，我暫時保持這樣。未來我可能會用旗標重新實作 system prompt 的部分。

**支援的安裝方式：** npm 和原生二進位檔（macOS 和 Linux）。

**重要**：如果你想保留你 patch 過的 system prompt，在 `~/.claude/settings.json` 加入以下設定來停用自動更新：

```json
{
  "env": {
    "DISABLE_AUTOUPDATER": "1"
  }
}
```

這適用於所有 Claude Code session，不管 shell 類型（interactive、non-interactive、tmux）。你可以在準備好對新版本重新套用 patch 時再手動更新。

### Lazy-load MCP 工具

如果你有使用 MCP server，它們的 tool definition 預設會載入到每段對話——即使你沒用到。這可能增加不少開銷，尤其是設定了多個 server 的時候。

啟用 lazy-loading 讓 MCP 工具只在需要時才載入：

```json
{
  "env": {
    "ENABLE_TOOL_SEARCH": "true"
  }
}
```

把這加到 `~/.claude/settings.json`。Claude 會按需搜尋和載入 MCP 工具，而不是從一開始就全部載入。從 2.1.7 版開始，當 MCP tool description 超過 context window 的 10% 時，這會自動發生。

## Tip 16: 用 Git worktree 平行處理分支

如果你同時在同一個專案做多件事又不想互相衝突，Git worktree 是個好方法。你只要叫 Claude Code 建一個 git worktree 然後在那邊工作就好——你不用擔心具體的語法。

基本概念是你可以在不同目錄裡的不同 branch 上工作。它本質上就是一個 branch + 一個目錄。

你可以在我在多工 tip 裡討論的瀑布式方法上加上 Git worktree 這一層。

### 什麼是 git worktree？

Git worktree 就像任何其他 git branch，但有一個專門指定給它的新目錄。

所以如果你在 main branch 和 feature-branch-1 上工作，沒有 git worktree 的話，你一次只能在一個上面工作，因為你的專案資料夾一次只能設定到一個 branch。

但有了 git worktree，你可以繼續在原始專案資料夾裡的 main branch（或任何其他 branch）工作，同時在新資料夾裡的 feature-branch-1 上工作。

![Git worktrees diagram showing parallel branch work in separate directories](assets/git-worktrees.png)

## Tip 17: 手動指數退避處理長時間任務

等待長時間任務（像 Docker build 或 GitHub CI）時，你可以叫 Claude Code 做手動指數退避（exponential backoff）。指數退避是軟體工程中常見的技術，但你也可以在這裡應用。叫 Claude Code 用越來越長的 sleep 間隔來檢查狀態——一分鐘、然後兩分鐘、然後四分鐘，以此類推。它不是在傳統意義上用程式做的——是 AI 手動做的——但效果很好。

這樣 agent 就能持續檢查狀態，完成時通知你。

（專門針對 GitHub CI，`gh run watch` 是存在的，但它持續輸出很多行，很浪費 token。用 `gh run view <run-id> | grep <job-name>` 做手動指數退避其實更省 token。這也是一個通用技術，就算沒有專門的等待指令也能用得很好。）

例如，如果你有一個 Docker build 在背景跑：

![Manual exponential backoff checking Docker build progress](assets/manual-exponential-backoff.png)

它會一直跑直到任務完成。

## Tip 18: 把 Claude Code 當寫作助手

Claude Code 是個很棒的寫作助手和夥伴。我用它寫作的方式是先給它關於我要寫什麼的所有 context，然後用語音給它詳細的指示。這就給了我第一份草稿。如果不夠好，我會試幾次。

然後我基本上逐行檢視。我說好，我們一起看看。我喜歡這一行，原因是這些。我覺得這一行需要移到那邊。這一行需要用這種特定方式修改。我也可能問一些參考資料。

所以就是這種來回的過程，也許終端機在左邊、程式碼編輯器在右邊：

![Side-by-side writing workflow with Claude Code](assets/writing-assistant-side-by-side.png)

這樣做效果通常很好。

## Tip 19: Markdown 超讚

一般人寫新文件時，可能會用 Google Docs 或 Notion 之類的。但現在我真心覺得最有效率的方式是 markdown。

Markdown 在 AI 之前就已經很好了，但特別是搭配 Claude Code，因為它在寫作方面很有效率（如我前面提到的），在我看來提高了 markdown 的價值。每當你想寫一篇部落格文章甚至 LinkedIn 貼文，你可以直接跟 Claude Code 說，讓它存成 markdown，然後從那邊繼續。

這裡有個小技巧：如果你想把 markdown 內容複製貼到一個不容易接受它的平台，你可以先貼到一個新的 Notion 檔案，然後從 Notion 複製到另一個平台。Notion 會轉換成其他平台可以接受的格式。如果一般貼上不行，試試 Command + Shift + V 來貼上不帶格式的版本。

## Tip 20: 用 Notion 保留貼上時的連結

反過來也行。如果你有從其他地方來的帶連結的文字，比方說從 Slack，你可以複製它。如果你直接貼到 Claude Code，它不會顯示連結。但如果你先放到 Notion 文件裡，再從那邊複製，你就能拿到 markdown 格式，Claude Code 當然讀得懂。

## Tip 21: 用容器跑長時間的高風險任務

一般的 session 比較適合有條理的工作，你控制給予的權限並更仔細地檢視輸出。容器化環境很適合 `--dangerously-skip-permissions` 的 session，你不用每個小東西都批准權限，就讓它自己跑一陣子。

這對研究或實驗很有用，那些需要很長時間而且可能有風險的事情。一個好例子是 Tip 11 的 Reddit 研究工作流程，reddit-fetch skill 透過 tmux 跟 Gemini CLI 來回。在你的主系統上讓它無監督地跑是有風險的，但在容器裡，就算出了什麼問題也是被隔離的。

另一個例子是我怎麼在這個 repo 裡做 [system prompt patching 腳本](system-prompt/)。當 Claude Code 出新版時，我需要更新壓縮過的 CLI bundle 的 patch。與其在我的主機上用 `--dangerously-skip-permissions` 跑 Claude Code（它能存取所有東西），我在容器裡跑。Claude Code 可以探索壓縮過的 JavaScript、找到變數映射、建立新的 patch 檔案，而我不用批准每一個小動作。

事實上，它幾乎能自己完成遷移。它試著套用 patch，發現有些在新版本上不行，迭代修復它們，甚至還改進了[說明文件](system-prompt/UPGRADING.md)供未來的 instance 參考。

我甚至做了 [SafeClaw](https://github.com/ykdojo/safeclaw) 來讓跑容器化的 Claude Code session 更簡單。它讓你啟動多個隔離的 session，每個都有一個 web terminal，然後從一個 dashboard 管理它們。它使用了這個 repo 的幾個自訂功能，包括優化過的 system prompt、[DX plugin](#tip-44-安裝-dx-plugin) 和[狀態列](#tip-0-自訂你的狀態列)。

### 進階：指揮容器裡的 worker Claude Code

你可以更進一步，讓你本機的 Claude Code 控制另一個跑在容器裡的 Claude Code instance。訣竅是用 tmux 作為控制層：

1. 你本機的 Claude Code 啟動一個 tmux session
2. 在那個 tmux session 裡，它跑或連接到容器
3. 容器裡面，Claude Code 用 `--dangerously-skip-permissions` 跑
4. 你外面的 Claude Code 用 `tmux send-keys` 送 prompt 和 `capture-pane` 讀取輸出

這給你一個完全自動的「worker」Claude Code，可以跑實驗性或長時間的任務，你不用批准每個動作。完成後，你本機的 Claude Code 可以把結果拉回來。如果出了什麼問題，全部都在容器的沙盒裡。

### 進階：多模型協調

不只是 Claude Code，你可以在容器裡跑不同的 AI CLI——Codex、Gemini CLI 或其他的。我試過 OpenAI Codex 做 code review，效果不錯。重點不是你不能直接在主機上跑這些 CLI——你當然可以。價值在於 Claude Code 的 UI/UX 流暢到你可以直接跟它說話，讓它處理協調工作：啟動不同的模型、在容器和主機之間傳資料。不用手動在終端機之間切換和複製貼上，Claude Code 變成了協調一切的中央介面。

## Tip 22: 學好 Claude Code 最好的方法就是一直用它

最近我看到一個世界級攀岩選手被另一個攀岩者訪問。她被問「你怎麼變得更會攀岩？」她簡單地說：「靠攀岩。」

我對這件事的感覺也一樣。當然，你可以做一些輔助的事，像看影片、讀書、學技巧。但用 Claude Code 是學怎麼用它的最好方式。一般來說，用 AI 是學怎麼用 AI 的最好方式。

我喜歡把它想成十億 token 法則，而不是一萬小時法則。如果你想精通 AI 並真正對它的運作方式建立良好的直覺，最好的方式就是消耗大量的 token。而且現在這是可能的。我發現尤其是用 Opus 4.5，它夠強大但又夠平價，你可以同時跑多個 session。你不用那麼擔心 token 用量，這讓你自由很多。

## Tip 23: Clone/fork 和 half-clone 對話

有時候你想從對話中的某個特定點嘗試不同的方法，又不想丟掉原來的對話。[clone-conversation 腳本](scripts/clone-conversation.sh)讓你可以用新的 UUID 複製一段對話，讓你可以分支出去。

**內建替代方案（較新版本）：** Claude Code 現在有原生的 fork 功能：
- `/fork` - 在對話中 fork 目前的 session
- `--fork-session` - 搭配 `--resume` 或 `--continue` 使用（例如 `claude -c --fork-session`）

因為 `--fork-session` 沒有簡寫形式，你可以在 `~/.zshrc` 或 `~/.bashrc` 加入這個 function，用 `--fs` 作為快捷鍵：

```bash
claude() {
  local args=()
  for arg in "$@"; do
    if [[ "$arg" == "--fs" ]]; then
      args+=("--fork-session")
    else
      args+=("$arg")
    fi
  done
  command claude "${args[@]}"
}
```

這會攔截所有 `claude` 指令，把 `--fs` 展開為 `--fork-session`，其他的原封不動傳過去。跟 alias 也能搭配使用（見 [Tip 7](#tip-7-設定終端機-alias-快速啟動)）：`c -c --fs`、`ch -c --fs` 等。

下面的 clone 腳本比這些內建選項更早出現，但下面的 half-clone 腳本仍然是獨特的，用來減少 context。

第一則訊息會標記 `[CLONED <timestamp>]`（例如 `[CLONED Jan 7 14:30]`），這在 `claude -r` 的列表和對話裡面都會顯示。

手動設定的話，把兩個檔案都建立 symlink：
```bash
ln -s /path/to/this/repo/scripts/clone-conversation.sh ~/.claude/scripts/clone-conversation.sh
ln -s /path/to/this/repo/skills/clone ~/.claude/skills/clone
```

或者透過 [dx plugin](#tip-44-安裝-dx-plugin) 安裝——不需要 symlink。

然後在任何對話中打 `/clone`（如果用 plugin 就是 `/dx:clone`），Claude 會處理找到 session ID 和跑腳本。

我已經廣泛測試過，clone 效果非常好。

### Half-clone 來減少 context

當對話太長時，[half-clone-conversation 腳本](scripts/half-clone-conversation.sh)只保留後半段。這在保留你最近工作的同時減少 token 用量。第一則訊息會標記 `[HALF-CLONE <timestamp>]`（例如 `[HALF-CLONE Jan 7 14:30]`）。

手動設定的話，把兩個檔案都建立 symlink：
```bash
ln -s /path/to/this/repo/scripts/half-clone-conversation.sh ~/.claude/scripts/half-clone-conversation.sh
ln -s /path/to/this/repo/skills/half-clone ~/.claude/skills/half-clone
```

或者透過 [dx plugin](#tip-44-安裝-dx-plugin) 安裝——不需要 symlink。

### 用 hook 自動建議 half-clone

你也可以選擇用一個 [hook](https://docs.anthropic.com/en/docs/claude-code/hooks) 來在 context 太滿時自動觸發 `/half-clone`。[check-context 腳本](scripts/check-context.sh)在每次 Claude 回覆後執行，檢查 context 用量。如果超過 85%，它會告訴 Claude 跑 `/half-clone`，建立一個只有後半段的新對話，讓新的 agent 可以在那裡繼續。

設定方式，先複製腳本：
```bash
cp /path/to/this/repo/scripts/check-context.sh ~/.claude/scripts/check-context.sh
chmod +x ~/.claude/scripts/check-context.sh
```

然後在你的 `~/.claude/settings.json` 加入 hook：
```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "~/.claude/scripts/check-context.sh"
          }
        ]
      }
    ]
  }
}
```

這需要停用 auto-compact（`/config` > Auto-compact > false），否則 Claude Code 可能在 hook 有機會觸發之前就壓縮 context 了。觸發時，hook 會阻止 Claude 停止並告訴它跑 `/half-clone`。相比 auto-compact 的優勢是 half-clone 是確定性的且很快——它保留你的實際訊息而不是摘要它們。

### 建議的 clone 腳本權限

兩個 clone 腳本都需要讀取 `~/.claude`（取得對話檔案和紀錄）。為了避免任何專案的權限提示，在你的全域設定（`~/.claude/settings.json`）加入：
```json
{
  "permissions": {
    "allow": ["Read(~/.claude)"]
  }
}
```

## Tip 24: 用 realpath 取得絕對路徑

當你需要告訴 Claude Code 不同資料夾裡的檔案時，用 `realpath` 取得完整的絕對路徑：

```bash
realpath some/relative/path
```

## Tip 25: 搞懂 CLAUDE.md、Skills、Slash Commands 和 Plugins 的差別

這些功能有點類似，我一開始覺得蠻困惑的。我一直在研究它們，盡力搞清楚，所以想分享我學到的。

**CLAUDE.md** 是最簡單的。它是一堆檔案，被當作預設的 prompt，在每段對話開始時載入，不管怎樣都會載入。好處在於簡單。你可以在特定專案（`./CLAUDE.md`）或全域（`~/.claude/CLAUDE.md`）中說明專案是關於什麼的。

**Skills** 就像結構更好的 CLAUDE.md 檔案。它們可以在相關時由 Claude 自動呼叫，或由使用者手動用 slash 呼叫（例如 `/my-skill`）。舉例來說，你可以有一個 skill，當你問某個語言怎麼發音時，它會用正確的格式打開 Google Translate 連結。如果那些指令在 skill 裡，它們只在需要時才載入。如果放在 CLAUDE.md 裡，它們已經在那裡佔空間了。所以理論上 skill 更省 token。

**Slash Commands** 跟 skill 類似，都是把指令分開打包的方式。使用者可以手動呼叫，Claude 自己也能呼叫。如果你需要更精確的控制，在你自己的節奏下在對的時機呼叫，slash command 就是該用的工具。

Skills 和 slash commands 在功能上蠻像的。差別在設計意圖——skill 主要是設計給 Claude 用的，slash command 主要是設計給使用者用的。不過，他們最後[把它們合併了](https://www.reddit.com/r/ClaudeAI/comments/1q92wwv/merged_commands_and_skills_in_213_update/)，這是我[建議的改動](https://github.com/anthropics/claude-code/issues/13115)。

**Plugins** 是把 skills、slash commands、agents、hooks 和 MCP server 打包在一起的方式。但一個 plugin 不一定要全部都用。Anthropic 官方的 `frontend-design` plugin 基本上就只是一個 skill。它可以作為獨立的 skill 發布，但 plugin 格式讓安裝更容易。

舉例來說，我做了一個叫 `dx` 的 plugin，把這個 repo 裡的 slash commands 和一個 skill 打包在一起。你可以在[安裝 dx plugin](#tip-44-安裝-dx-plugin) 章節看它怎麼運作。

## Tip 26: 互動式 PR review

Claude Code 很適合做 PR review。流程很簡單：你叫它用 `gh` 指令取得 PR 資訊，然後你想怎麼 review 就怎麼 review。

你可以做一般性的 review，或者一個檔案一個檔案、一步一步來。你控制節奏。你控制你想看多少細節和工作的複雜度。也許你只想了解整體結構，或者你也想讓它跑測試。

關鍵差異是 Claude Code 是一個互動式的 PR reviewer，而不只是一次性的機器。有些 AI 工具擅長一次性 review（包括最新的 GPT 模型），但用 Claude Code 你可以對話。

## Tip 27: 把 Claude Code 當研究工具

Claude Code 對任何研究來說都很厲害。它基本上是 Google 或 deep research 的替代品，但在幾個方面更先進。不管你是在研究為什麼某些 GitHub Actions 失敗了（我最近一直在做這個）、在 Reddit 上做情緒或市場分析、探索你的 codebase、或是搜尋公開資訊——它都能做到。

關鍵是給它正確的資訊和關於如何存取那些資訊的指示。可能是 `gh` 終端指令存取、或容器方法（Tip 21）、或透過 Gemini CLI 的 Reddit（Tip 11）、或透過 MCP 的私人資訊（像 Slack MCP）、或 Cmd+A / Ctrl+A 方法（Tip 10）——不管是什麼。此外，如果 Claude Code 載入某些 URL 有困難，你可以試試 Playwright MCP 或 Claude 的原生瀏覽器整合（見 Tip 9）。對於學術研究，我做了一個 [paper-search](https://github.com/ykdojo/paper-search) plugin 來搜尋學術論文。

事實上，我甚至能[用 Claude Code 做研究省下 $10,000](content/how-i-saved-10k-with-claude-code.md)。

## Tip 28: 精通各種驗證輸出的方法

驗證輸出的一個方法，如果是程式碼的話，就是讓它寫測試並確保測試整體上看起來沒問題。這是一種方法，但你當然也可以在 Claude Code UI 上邊看它生成的程式碼邊檢查。另一個是你可以用視覺化的 Git 客戶端，像 GitHub Desktop。我個人就在用。它不是完美的產品，但夠好用來快速檢查改動。讓它生成 PR 也是個好方法，我大概在這篇文章前面提過了。讓它建 draft PR，在轉成正式 PR 之前先檢查內容。

另一個是讓它自己檢查自己的工作。如果它給你某種輸出，比方說來自某個研究的，你可以說「你確定嗎？你能 double check 嗎？」我最喜歡的 prompt 之一是說「double check 所有東西，你產出的每一個聲明，最後做一個表格列出你能驗證的東西」——這似乎效果非常好。

## Tip 29: 把 Claude Code 當 DevOps 工程師

我想專門為這個做一個獨立的 tip，因為這對我來說真的很驚人。每當有 GitHub Actions CI 失敗，我就直接丟給 Claude Code 說「深入研究這個問題，試著找到根本原因。」有時候它給你表面的答案，但如果你繼續追問——是某個特定的 commit、某個特定的 PR 造成的，還是偶發問題？——它真的能幫你深入這些手動很難挖的麻煩問題。你需要翻一堆 log，手動做超級痛苦，但 Claude Code 能處理很多。

我把這個工作流程包成了一個 `/gha` slash command——只要跑 `/gha <url>` 加上任何 GitHub Actions URL，它就會自動調查失敗原因、檢查是否為偶發、找出導致問題的 commit，並建議修復方式。你可以在 [skills 資料夾](skills/gha/SKILL.md)找到它，或透過 [dx plugin](#tip-44-安裝-dx-plugin) 安裝。

一旦你找出特定的問題，你就可以建 draft PR 然後用我前面提到的一些技巧——檢查輸出、確保看起來沒問題、讓它驗證自己的輸出，然後轉成正式 PR 來真正修復問題。這對我個人來說效果真的很好。

## Tip 30: 保持 CLAUDE.md 簡潔並定期檢視

保持 CLAUDE.md 簡潔並盡可能精簡很重要。你可以完全不用 CLAUDE.md 開始。如果你發現你一直在跟 Claude Code 說同樣的話，就把它加到 CLAUDE.md。我知道有個透過 `#` 符號的選項可以做到，但我比較喜歡直接叫 Claude Code 加到專案層級的 CLAUDE.md 或全域的 CLAUDE.md，它會知道要編輯什麼。

![Keep it simple meme](assets/keep-it-simple-meme.jpg)

定期檢視你的 CLAUDE.md 檔案也很重要，因為它們會隨時間過期。之前合理的指示可能不再相關，或者你可能有新的模式應該被記錄。我為此做了一個叫 [`review-claudemd`](skills/review-claudemd/SKILL.md) 的 skill，它會分析你最近的對話並建議改進你的 CLAUDE.md 檔案。

## Tip 31: Claude Code 作為萬用介面

我以前覺得用 Claude Code 時，CLI 就像新的 IDE，某種程度上這還是對的。我覺得它是你想做快速編輯之類的時候，打開專案的好地方。但取決於你專案的嚴肅程度，你會想比只停在 vibe coding 的層級更仔細地檢查輸出。

但同樣真實的是——更廣義地說——Claude Code 真的是你電腦、數位世界、任何數位問題的萬用介面。很多情況你可以讓它自己搞定。例如，如果你需要快速剪一段影片，直接叫它做——它大概會用 ffmpeg 或類似的東西搞定。如果你想轉錄一堆你本機的音檔或影片檔，直接叫它做——它可能會建議用 Python 的 Whisper。如果你想分析 CSV 裡的資料，它可能會建議用 Python 或 JavaScript 來視覺化。當然再加上網路存取——Reddit、GitHub、MCP——可能性是無限的。

它對你想在本機電腦上做的任何操作也很棒。例如，如果你快沒有儲存空間了，直接叫它給你一些清理建議。它會檢視你的本機資料夾和檔案，試著找出什麼佔了很多空間，然後給你清理的建議——也許刪掉特別大的檔案。以我的例子來說，我有一些 Final Cut Pro 的檔案真的很大，我早該清掉了。Claude Code 告訴我了。也許它會告訴你用 `docker system prune` 清理沒在用的 Docker image 和 container。或者告訴你清掉你從來不知道還在那裡的某個 cache。不管你想在電腦上做什麼，Claude Code 現在是我第一個去的地方。

我覺得蠻有趣的，因為電腦一開始就是文字介面。而我們在某種意義上回到了這個文字介面，你可以同時開三四個分頁，如我之前提到的。對我來說這真的很興奮。感覺你有了第二個大腦。但因為它的結構方式——就是一個終端機分頁——你可以開第三個大腦、第四個大腦、第五個大腦、第六個大腦。隨著模型變得更強大，你能委派給這些東西的思考比例——不是重要的事情，而是你不想做的或覺得無聊或太瑣碎的事情——你可以讓它們處理。如我提到的，一個好例子就是看 GitHub Actions。誰想做那個？但事實證明這些 agent 真的很擅長那些無聊的任務。

## Tip 32: 關鍵在於選擇對的抽象層級

如我之前提到的，有時候停在 vibe coding 的層級是可以的。如果你在做一次性的專案或 codebase 裡不關鍵的部分，你不一定需要擔心每一行程式碼。但其他時候，你會想挖深一點——看看檔案結構和函式、個別的程式碼行，甚至檢查 dependency。

![Vibe coding spectrum](assets/vibe-coding-spectrum.png)

關鍵是這不是二元的。有些人說 vibe coding 不好因為你不知道自己在做什麼，但有時候完全沒問題。但其他時候，挖深一點、運用你的軟體工程技能、在更細的層級理解程式碼，或者複製貼上 codebase 的某些部分或特定的 error log 來問 Claude Code 具體問題，確實是有幫助的。

就像你在探索一座巨大的冰山。如果你想停在 vibe coding 層級，你可以飛過頂部從遠處看。然後你可以靠近一點。你可以進入潛水模式。你可以越潛越深，讓 Claude Code 當你的嚮導。

## Tip 33: 審查你已批准的指令

我最近看到[這篇文章](https://www.reddit.com/r/ClaudeAI/comments/1pgxckk/claude_cli_deleted_my_entire_home_directory_wiped/)，有人的 Claude Code 跑了 `rm -rf tests/ patches/ plan/ ~/` 然後把他的 home 目錄全刪了。很容易把這當作 vibe coder 的錯誤而忽略，但這種錯誤任何人都可能遇到。所以定期審查你已批准的指令很重要。為了讓這更容易，我做了 **cc-safe**——一個掃描你 `.claude/settings.json` 裡危險已批准指令的 CLI 工具。

它能偵測像這樣的模式：
- `sudo`、`rm -rf`、`Bash`、`chmod 777`、`curl | sh`
- `git reset --hard`、`npm publish`、`docker run --privileged`
- 還有更多——它能辨識容器環境所以 `docker exec` 的指令會被跳過

它會遞迴掃描所有子目錄，所以你可以指向你的專案資料夾一次檢查所有東西。你可以手動跑或叫 Claude Code 幫你跑：

```bash
npm install -g cc-safe
cc-safe ~/projects
```

或者直接用 npx 跑：

```bash
npx cc-safe .
```

GitHub：[cc-safe](https://github.com/ykdojo/cc-safe)

## Tip 34: 多寫測試（用 TDD）

隨著你用 Claude Code 寫越多程式碼，越容易犯錯。PR review 和視覺化 Git 客戶端能幫忙抓問題（如我之前提到的），但當你的 codebase 越來越大時，寫測試就變得至關重要。

你可以讓 Claude Code 為自己的程式碼寫測試。有些人說 AI 不能測試自己的作品，但事實上它可以——跟人類大腦的運作方式類似。當你寫測試時，你用不同的方式思考同一個問題。AI 也一樣。

我發現 TDD（Test-Driven Development，測試驅動開發）跟 Claude Code 搭配得非常好：

1. 先寫測試
2. 確認測試會失敗
3. Commit 測試
4. 寫程式碼讓它們通過

這其實就是我做 [cc-safe](https://github.com/ykdojo/cc-safe) 的方式。先寫會失敗的測試然後在實作前 commit，你就為程式碼應該做什麼建立了一個清楚的契約。Claude Code 就有一個明確的目標可以達成，你也可以跑測試來驗證實作是否正確。

如果你想更確定，自己 review 測試確保它們沒做什麼蠢事，像是直接回傳 true。

## Tip 35: 在未知領域更勇敢一點；迭代式解決問題

自從我開始更密集地使用 Claude Code 後，我注意到我在未知領域變得越來越勇敢。

例如，我開始在 [Daft](https://github.com/Eventual-Inc/Daft) 工作時，注意到我們前端程式碼的一個問題。我不是 React 專家，但我還是決定深入研究。我就開始問關於 codebase 和問題的問題。最後我能解決它，因為我知道怎麼用 Claude Code 迭代式地解決問題。

最近也發生了類似的事。我在為 Daft 的使用者做一份指南，遇到了一些非常具體的問題：cloudpickle 在 Google Colab 跟 Pydantic 配合不了，還有一個 Python 和一點 Rust 的問題，東西在 JupyterLab 裡印不出來但在終端機裡正常。我之前從來沒寫過 Rust。

我本來可以只建一個 issue 讓其他工程師處理。但我想，讓我深入 codebase 看看。Claude Code 給了一個初步的解決方案，但不夠好。所以我放慢速度。一個同事建議我們就把那部分停用，但我不想有任何退步。我們能找到更好的解決方案嗎？

接下來是一個協作和迭代的過程。Claude Code 建議可能的根因和解決方案。我實驗那些方案。有些走到死胡同，所以我們換了方向。整個過程中，我控制自己的節奏。有時候快一點，像是讓它探索不同的解決方案空間或 codebase 的不同部分。有時候慢一點，問「這一行到底什麼意思？」控制抽象層級，控制速度。

最後我找到了一個蠻優雅的解決方案。教訓是：即使在未知的世界裡，你用 Claude Code 能做的比你想像的多很多。

## Tip 36: 在背景執行 bash 指令和 subagent

當 Claude Code 裡有一個長時間執行的 bash 指令時，你可以按 Ctrl+B 把它移到背景執行。Claude Code 知道怎麼管理背景行程——它可以之後用 BashOutput 工具來檢查。

這在你發現一個指令比預期久，而你想讓 Claude 同時做別的事情時很有用。你可以讓它用我在 Tip 17 提到的指數退避方法來檢查進度，或者讓它在行程跑的同時做完全不同的事情。

Claude Code 也有能力在背景跑 subagent。如果你需要做長時間的研究或讓一個 agent 定期檢查某個東西，你不用讓它在前景跑。只要叫 Claude Code 在背景跑一個 agent 或任務，它就會在你繼續其他工作時處理。

### 策略性地使用 subagent

不只是在背景跑東西，subagent 在你有大型任務要拆分時也很有用。例如，如果你有一個巨大的 codebase 需要分析，你可以讓 subagent 用不同的方式分析它，或者平行地看 codebase 的不同部分。只要叫 Claude 產生多個 subagent 來處理不同的部分。

你可以透過直接要求來自訂 subagent：
- **數量** - 叫 Claude 產生你想要的數量
- **背景 vs 前景** - 叫它在背景跑，或按 Ctrl+B
- **用哪個模型** - 根據每個任務的複雜度要求用 Opus、Sonnet 或 Haiku（subagent 預設用 Sonnet）

## Tip 37: 個人化軟體的時代來了

我們正在進入個人化、客製軟體的時代。自從 AI 出來——一般的 ChatGPT，但尤其是 Claude Code——我注意到我能製作更多的軟體了，有時候只是給自己用，有時候是小專案。

如我之前在這份文件中提到的，我做了一個每天都用來跟 Claude Code 說話的自訂轉錄工具。我做了自訂 Claude Code 本身的方法。我也用 Python 做了一堆資料視覺化和分析的任務，比我自己做快得多。

再舉一個例子：[korotovsky/slack-mcp-server](https://github.com/korotovsky/slack-mcp-server)，一個快 1,000 顆星的熱門 Slack MCP，設計成跑在 Docker container 裡。我在自己的 Docker container 裡用它遇到困難（Docker-in-Docker 的問題）。與其跟那個設定搏鬥，我直接叫 Claude Code 用 Slack 的 Node SDK 寫一個 CLI。效果很好。

這是一個令人興奮的時代。不管你想完成什麼，都可以叫 Claude Code 來做。如果夠小，你可以在一兩個小時內做好。我甚至做了一個[簡報模板](https://ykdojo.github.io/claude-code-tips/content/spectrum-slides.html)——一個包含 CSS 和 JavaScript 的單一 HTML 檔案，讓你可以在裡面嵌入一個互動式、持續的終端機行程。

## Tip 38: 在輸入框裡移動和編輯

Claude Code 的輸入框設計成模擬常見的終端機/readline 快捷鍵，如果你習慣在終端機工作的話會覺得很自然。以下是一些有用的：

**移動：**
- `Ctrl+A` - 跳到行首
- `Ctrl+E` - 跳到行尾
- `Option+Left/Right`（Mac）或 `Alt+Left/Right` - 按單字向前/向後跳

**編輯：**
- `Ctrl+W` - 刪除前一個單字
- `Ctrl+U` - 從游標刪到行首
- `Ctrl+K` - 從游標刪到行尾
- `Ctrl+C` / `Ctrl+L` - 清除目前的輸入
- `Ctrl+G` - 在外部編輯器打開你的 prompt（對貼上長文字很有用，因為直接貼到終端機可能很慢）

如果你熟悉 bash、zsh 或其他 shell，你會覺得很有家的感覺。

`Ctrl+G` 的編輯器由你的 `EDITOR` 環境變數決定。你可以在 shell 設定檔（`~/.zshrc` 或 `~/.bashrc`）設定：

```bash
export EDITOR=vim      # or nano, code, nvim, etc.
```

或在 `~/.claude/settings.json`（需要重新啟動）：

```json
{
  "env": {
    "EDITOR": "vim"
  }
}
```

**輸入換行（多行輸入）：**

最快的方法在任何地方都能用，不需要任何設定：打 `\` 然後按 Enter 就能建立換行。如果要用鍵盤快捷鍵，在 Claude Code 裡跑 `/terminal-setup`。在 Mac 的 Terminal.app 上，我用 Option+Enter。

**貼上圖片：**
- `Ctrl+V`（Mac/Linux）或 `Alt+V`（Windows）- 從剪貼簿貼上圖片

注意：在 Mac 上是 `Ctrl+V`，不是 `Cmd+V`。

## Tip 39: 花點時間規劃，但也要快速做原型

你要花夠多的時間規劃，讓 Claude Code 知道要做什麼以及怎麼做。這意味著早期就做好高層的決定：用什麼技術、專案應該怎麼架構、每個功能應該放在哪裡、東西應該放在哪些檔案裡。盡早做好決定是重要的。

有時候做原型對此有幫助。只要快速做一個簡單的原型，你可能就能說「好，這個技術對這個特定目的有用」或「這個其他技術更好」。

例如，我最近在實驗做一個 diff viewer。我先試了一個用 tmux 和 lazygit 的簡單 bash 原型，然後試著用 Ink 和 Node 做自己的 git viewer。我在各種事情上遇到很多困難，最後沒有發布任何成果。但我從這個專案中被重新提醒的是規劃和原型的重要性。我發現只要在讓它寫程式碼之前多規劃一下，你就能更好地引導它。你在整個寫程式的過程中仍然需要引導它，但先讓它規劃一下真的很有幫助。

你可以用 plan mode 來做，按 Shift+Tab 切換到它。或者你可以直接叫 Claude Code 在寫任何程式碼之前先做一個計畫。

## Tip 40: 簡化過度複雜的程式碼

我發現 Claude Code 有時候會把事情弄得太複雜，寫太多程式碼。它會做你沒要求的改動。它似乎就是傾向寫更多程式碼。如果你有照這份指南的其他技巧做的話，程式碼可能能正確運作，但會很難維護、很難檢查。如果你 review 不夠的話，可能是場噩夢。

所以有時候你要檢查程式碼並叫它簡化。你可以自己修，但你也可以叫它簡化。你可以問像「你為什麼做了這個特定的改動？」或「你為什麼加了這一行？」

有些人說如果你只透過 AI 寫程式碼，你永遠不會理解它。但這只有在你問的問題不夠多時才成立。如果你確保理解每一個東西，你實際上可以比平常更快理解程式碼，因為你可以問 AI 。尤其是在做大型專案的時候。

注意這也適用於散文。Claude Code 經常試著在最後一段總結前面的段落，或在最後一句總結前面的句子。它可以變得相當重複。有時候這有幫助，但大多數時候你會需要叫它刪掉或簡化。

## Tip 41: 自動化的自動化

歸根結底，一切都是關於自動化的自動化。我的意思是，我發現這是不只提高生產力、還能讓過程更有趣的最好方式。至少對我來說，這整個自動化的自動化過程真的很有趣。

我個人從 ChatGPT 開始，想要自動化複製貼上和跑 ChatGPT 給我的指令到終端機的過程。我透過做一個叫 [Kaguya](https://github.com/ykdojo/kaguya) 的 ChatGPT plugin 自動化了整個流程。從那以後我一直朝著越來越多的自動化前進。

現在幸運的是，我們甚至不用自己做那種工具了，因為像 Claude Code 這樣的工具存在而且效果很好。隨著我用得越來越多，我開始想，如果我能自動化打字的過程呢？所以我用 Claude Code 本身做了我的語音轉錄 app，如我之前提到的。

然後我開始想，我發現自己有時候在重複。所以我會把那些東西放到 CLAUDE.md。然後我會想，好，有時候我一直跑同一個指令。怎麼自動化？也許我可以叫 Claude Code 來做。或者把它們放到 skill 裡。或者甚至讓它建一個腳本，這樣我就不用一再重複同樣的過程。

我覺得這終究是我們的方向。每當你發現自己一再重複同一個任務或指令，重複幾次沒關係，但如果你一直重複，就想個辦法自動化整個過程。

## Tip 42: 分享你的知識，能貢獻就貢獻

這個 tip 跟其他的有點不同。我發現透過盡可能多學，你就能把知識分享給周圍的人。也許透過像這樣的文章，也許甚至是書、課程、影片。我最近也在 Daft 為同事辦了一場[內部分享](https://www.daft.ai/blog/how-we-use-ai-coding-agents)。非常有收穫。

每當我分享技巧時，我常常也會得到資訊回饋。例如，當我分享我的縮短 system prompt 和 tool description 的技巧（Tip 15）時，有些人告訴我可以用 `--system-prompt` 旗標作為替代。另一次，我分享了 slash command 和 skill 的差別（Tip 25），我從那篇 Reddit 貼文的留言中學到了新東西。

所以分享你的知識不只是建立個人品牌或鞏固學習。它也是透過這個過程學新東西。這不一定是單向的。

說到貢獻，我一直在 Claude Code 的 repo 提 issue。我想，好，如果他們聽就太好了。如果不聽，完全沒問題。我沒有任何期待。但在 2.0.67 版中，我注意到他們採納了我提出的多個建議：

- 修復了在 `/permissions` 中刪除權限規則後捲動位置重置的問題
- 在 `/permissions` 指令中加入了搜尋功能

他們團隊對功能請求和 bug 回報的反應速度真的很驚人。但這也說得通，因為他們就是在用 Claude Code 來做 Claude Code 本身。

## Tip 43: 持續學習！

有幾個有效的方式可以持續學習 Claude Code：

**問 Claude Code 本身** - 如果你有關於 Claude Code 的問題，直接問它。Claude Code 有一個專門的 subagent 來回答關於它自己的功能、slash command、設定、hooks、MCP server 等等的問題。

**看 release notes** - 打 `/release-notes` 來看你目前版本有什麼新東西。這是學最新功能的最好方式。

**向社群學習** - [r/ClaudeAI](https://www.reddit.com/r/ClaudeAI/) subreddit 是個從其他使用者學習和看大家用什麼工作流程的好地方。

**追蹤 Ado 的技巧** - Ado（[@adocomplete](https://x.com/adocomplete)）是 Anthropic 的 DevRel，在 2025 年 12 月整個月都在他的「Advent of Claude」系列中發布每日 Claude Code 技巧。雖然這個特定系列已經結束了，但他持續在 X 上分享有用的技巧。

- [Twitter/X: Advent of Claude 貼文](https://x.com/search?q=from%3Aadocomplete%20advent%20of%20claude&src=typed_query&f=live)
- [LinkedIn: Advent of Claude 貼文](https://www.linkedin.com/search/results/content/?fromMember=%5B%22ACoAAAFdD3IBYHwKSh6FsyGqOh1SpbrZ9ZHTjnI%22%5D&keywords=advent%20of%20claude&origin=FACETED_SEARCH&sid=zDV&sortBy=%22date_posted%22)

## Tip 44: 安裝 dx plugin

這個 repo 也是一個叫 `dx`（developer experience）的 Claude Code plugin。它把上面幾個 tip 的工具打包成一個安裝：

| Skill | 說明 |
|-------|-------------|
| `/dx:gha <url>` | 分析 GitHub Actions 失敗（Tip 29） |
| `/dx:handoff` | 建立 handoff 文件確保 context 延續（Tip 8） |
| `/dx:clone` | Clone 對話來分支（Tip 23） |
| `/dx:half-clone` | Half-clone 來減少 context（Tip 23） |
| `/dx:reddit-fetch` | 透過 Gemini CLI 抓 Reddit 內容（Tip 11） |
| `/dx:review-claudemd` | 檢視對話來改善 CLAUDE.md 檔案（Tip 30） |

**兩個指令就能安裝：**

```bash
claude plugin marketplace add ykdojo/claude-code-tips
claude plugin install dx@ykdojo
```

安裝後，這些指令就能用了：`/dx:clone`、`/dx:half-clone`、`/dx:handoff` 和 `/dx:gha`。`reddit-fetch` skill 會在你問 Reddit URL 時自動呼叫。`review-claudemd` skill 會分析你最近的對話並建議改善你的 CLAUDE.md 檔案。Clone 指令請看[建議的權限設定](#建議的-clone-腳本權限)。

**建議搭配：** [Playwright MCP](https://github.com/microsoft/playwright-mcp) 用於瀏覽器自動化——用 `claude mcp add -s user playwright npx @playwright/mcp@latest` 新增

## Tip 45: 快速設定腳本

如果你想一次設定這個 repo 的多個建議，有一個設定腳本可以處理很多：

```bash
bash <(curl -s https://raw.githubusercontent.com/ykdojo/claude-code-tips/main/scripts/setup.sh)
```

這個腳本會顯示它要設定的所有東西，讓你跳過任何項目：

```
INSTALLS:
  1. DX plugin - slash commands (/dx:gha, /dx:clone, /dx:handoff) and skills (reddit-fetch)
  2. cc-safe - scans your settings for risky approved commands like 'rm -rf' or 'sudo'

SETTINGS (~/.claude/settings.json):
  3. Status line - shows model, git branch, uncommitted files, token usage at bottom of screen
  4. Disable auto-updates - prevents Claude Code from auto-updating (useful for system prompt patches)
  5. Lazy-load MCP tools - only loads MCP tool definitions when needed, saves context
  6. Read(~/.claude) permission - allows clone/half-clone commands to read conversation history
  7. Read(//tmp/**) permission - allows reading temporary files without prompts
  8. Disable attribution - removes Co-Authored-By from commits and attribution from PRs

SHELL CONFIG (~/.zshrc or ~/.bashrc):
  9. Aliases: c=claude, ch=claude --chrome, cs=claude --dangerously-skip-permissions
 10. Fork shortcut: --fs expands to --fork-session (e.g., claude -c --fs)

Skip any? [e.g., 1 4 7 or Enter for all]:
```

---

📺 **相關演講**: [Claude Code Masterclass](https://youtu.be/9UdZhTnMrTA) - 來自 31 個月 agentic coding 的經驗和專案範例

📝 **故事**: [我如何用 Claude Code 找到全職工作](content/how-i-got-a-job-with-claude-code.md)

📰 **電子報**: [Agentic Coding with Discipline and Skill](https://agenticcoding.substack.com/) - 把 agentic coding 的實踐帶到更高的層次
