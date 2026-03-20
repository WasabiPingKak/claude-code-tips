# Agentic coding 的光譜：從 vibe coding 到高品質軟體工程

在過去兩年半裡，我在 AI 輔助寫程式上花了超過十億個 token——從我建立第一個 agentic coding 工具 [Kaguya](https://github.com/ykdojo/kaguya) 開始——我得出了一個體悟：vibe coding 和傳統軟體工程不是對立的。你可以透過注入你的軟體工程知識和傳統軟體工程實踐來強化 vibe coding。這樣一來，vibe coding 就變成了*有紀律的 agentic coding*、*agentic 軟體工程*，最終就只是高品質軟體工程。換句話說，vibe coding 是一個光譜。

![Agentic coding 的光譜](https://raw.githubusercontent.com/ykdojo/claude-code-tips/main/content/spectrum-chart.png)

## Agentic/vibe coding 的四個層級

![50 shades of agentic coding](https://raw.githubusercontent.com/ykdojo/claude-code-tips/main/content/50-shades-of-agentic-coding.jpeg)

### 第一級：Vibe coding

最淺的層次，vibe coding 就是你忘了程式碼的存在。你就讓 AI 隨便搞，讓它寫、寫、寫。錯誤 log？連看都不看——直接丟給 AI。讓 AI 處理一切。

版本控制？那是什麼？安全性？嗯，我晚上有鎖門啦。

這個層級對於一次性的專案、快速原型、用完即丟的腳本來說完全沒問題。但不要期望它長期可維護。

### 第二級：有紀律的 agentic coding

在這個層級，你開始引入一些結構：

- **版本控制**：你有在用 Git 和 GitHub 或類似的工具
- **檔案層級的理解**：你大概知道每個檔案在做什麼，以及它們之間如何互動
- **基本的安全防護**
- **測試**：你確保你的 app 在大多數情況下真的能動

### 第三級：Agentic 軟體工程

這是開始能上 production（正式環境）的階段。

- **測試**：不管是 AI 寫的還是人寫的，但你會驗證它們真的在測試該測的東西。你不一定每一行都看，但你確保它們看起來沒問題。
- **Pre-commit hook**：這解決了很多我有時看到人們用 Claude Code hook 來處理的問題——格式化問題、linting、簡單的檢查。
- **CI job**：用於持續測試
- **函式層級的理解**：你知道每個 class 和 function 在做什麼。你可能不會讀每一行，但你的理解比檔案層級更深。
- **品質控管措施**：仔細的手動測試、end-to-end 測試、一次性的 AI code review、regression 檢查

### 第四級：高品質軟體工程

雖然這仍然是 AI 輔助寫程式，但品質跟由 staff engineer 手寫的程式碼沒有區別——理想情況下速度更快。

- **逐行理解**：送 PR 時，你可能會先送一個 draft，確保每一行都是正確的、合理的
- **自我反思迴圈**：透過問「你確定嗎？那這些不同的方法呢？」之類的問題，你可以讓模型反思自己，抓出自己的錯誤，並進行大方向的權衡討論。
- **AI 驅動的互動式 code review**：不只是一次性的 AI review。你把改動拉到本地，先確保它們能跑。然後你針對每個檔案、函式、class，甚至個別行來詢問 AI——需要多深就挖多深。
- **進階研究方法**：用於架構決策：
  - Postgres vs. Cassandra？
  - AWS vs. Google Cloud vs. Render？
  - 在 Mac 上跑本地轉錄模型的最佳方式？

  你用 deep research 或 Claude Code 搭配 web search 和 [Reddit fetch](https://github.com/ykdojo/claude-code-tips?tab=readme-ov-file#tip-11-use-gemini-cli-as-a-fallback-for-blocked-sites) 來做研究，但必要時也會去確認來源。
- **AI 驅動的品質控管**：除了前面討論過的一切，你可能還會有像是[背景 Claude Code 任務來測試你的 CLI](https://github.com/ykdojo/claude-code-tips?tab=readme-ov-file#tip-9-complete-the-write-test-cycle-for-autonomous-tasks)（如果你在做 CLI 的話），或者[讓有瀏覽器存取權限的 AI 測試你的 UI](https://github.com/ykdojo/claude-code-tips?tab=readme-ov-file#creative-testing-strategies)（如果你在做 web app 的話）。此外，你可能還會做像是跨平台測試（Windows、Linux、Mac）、安全性和效能檢查等等。
- **加速學習**：不只是讓 AI 寫程式碼，你會問「你為什麼這樣寫？」或「這一行具體是什麼意思？」之類的問題。基本上，你是用 AI 來加深你的領域專業，而不是讓它什麼都包辦。

## Agentic coding 矩陣

總結一下，我建立了這個簡單的矩陣作為這四個層級的速查表：

| 層級 | 程式碼品質 | 速度 | 測試 | Code Review |
|-------|-----------|------|------|-------------|
| **Vibe Coding** | 低 | 閃電般 | 最低限度 | 無 |
| **有紀律的 Agentic Coding** | 尚可 | 較快 | 足夠 | 簡略 |
| **Agentic 軟體工程** | 中等 | 快 | 徹底 | 一次性 |
| **高品質軟體工程** | 高 | 不錯 | 堅如磐石 | 互動式 |

## 保持彈性

說到底，你應該精通這四個層級，並且靈活地選擇使用哪一個。

有時候停在 vibe coding 的層級就好——快速原型、一次性腳本、實驗。有時候你需要高品質軟體工程——醫療軟體、大規模系統、其他關鍵任務軟體。

你的程式碼第一版可能是「垃圾」——低品質的 AI 生成程式碼。沒關係。你可以在送 PR 或把 draft PR 標記為 ready 之前逐步改善它。

## 「垃圾程式碼」的真正問題

![關於 AI 輔助寫程式的 Midwit meme](https://raw.githubusercontent.com/ykdojo/claude-code-tips/main/content/midwit-meme.png)

大家抱怨 AI 生成的程式碼是垃圾。但問題是，它之所以是垃圾，是因為他們沒有花夠多功夫在上面。

花更多 token 不一定意味著你製造更多垃圾。取決於你怎麼用 AI，它也可以代表更高品質的程式碼、更好的研究，以及對你自己工作更深的理解。
