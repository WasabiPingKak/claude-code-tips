# Claude Code 創作者 Boris 的 10 個技巧摘要

Claude Code 的創作者 Boris Cherny 最近在 [X 上分享了 10 個技巧](https://x.com/bcherny/status/2017742741636321619)，來源是 Claude Code 團隊。以下是我透過 Claude Code 和 Opus 4.5 整理的快速摘要。

## 1. 多做平行作業

開 3-5 個 git worktree，每個跑自己的 Claude session。這是團隊裡最大的生產力提升。有些人設了 shell alias（za、zb、zc）來一鍵切換 worktree。

## 2. 每個複雜任務都從 plan mode 開始

把精力投入在計畫上，這樣 Claude 就能一次搞定實作。如果出了問題，切回 plan mode 重新規劃，而不是硬著頭皮繼續。有人甚至開第二個 Claude 來以 staff engineer 的角度審查計畫。

## 3. 好好經營你的 CLAUDE.md

每次糾正之後，告訴 Claude：「更新你的 CLAUDE.md，這樣你就不會再犯同樣的錯。」Claude 特別擅長幫自己寫規則。持續迭代，直到 Claude 的犯錯率明顯下降。

## 4. 建立自己的 skill 並 commit 到 git

如果你一天做某件事超過一次，就把它變成一個 skill 或 slash command（斜線命令）。團隊的例子：一個 `/techdebt` 命令來找重複的程式碼、一個把 Slack/GDrive/Asana/GitHub 同步成一份 context dump 的命令，還有寫 dbt model 的分析 agent。

## 5. Claude 自己能修大部分的 bug

把 Slack 上的 bug 討論串貼給 Claude，然後說「修。」或者說「去修那些失敗的 CI 測試。」不要微管理怎麼修。你也可以把 docker log 丟給 Claude 來排查分散式系統的問題。

## 6. 提升你的 prompting 技巧

挑戰 Claude——說「好好考考我這些改動，在我通過你的測試之前不要開 PR。」在一個平庸的修復之後，說「根據你現在知道的一切，丟掉這個，實作那個優雅的方案。」寫詳細的 spec 並減少模糊空間——越具體，輸出越好。

## 7. Terminal 和環境設定

團隊愛用 Ghostty。用 `/statusline` 來顯示 context 使用量和 git branch。用顏色標記你的 terminal 分頁。用語音輸入——你說話的速度是打字的 3 倍（在 macOS 上按兩次 fn 鍵）。

## 8. 使用 subagent（子代理）

當你想讓 Claude 投入更多運算資源時，說「use subagents」。把任務分配給 subagent 來保持你主要的 context window 乾淨。你也可以透過 hook 把權限請求導向 Opus 4.5 來自動批准安全的操作。

## 9. 用 Claude 做資料和分析

用 Claude 搭配 `bq` CLI（或任何資料庫 CLI/MCP/API）來拉取和分析指標。Boris 說他已經超過 6 個月沒寫過一行 SQL 了。

## 10. 用 Claude 來學習

在 `/config` 裡啟用「Explanatory」或「Learning」輸出風格，讓 Claude 解釋它改動背後的原因。你也可以讓 Claude 產生視覺化的 HTML 簡報、畫 ASCII 的程式碼架構圖，或建立一個 spaced-repetition（間隔重複）學習 skill。

---

我對很多這些技巧都很有共鳴，所以我建議至少試試其中幾個。如果你想看更多 Claude Code 技巧，我有一個收集了 45 個自己的技巧的 repo 在這裡：[claude-code-tips](https://github.com/ykdojo/claude-code-tips)
