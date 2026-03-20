# 給新手的 10 個 Claude Code 技巧

最近我發現越來越多人第一次嘗試 Claude Code 和 Cowork，所以我想給他們一些入門的建議。

完整的 45 個技巧合集：https://github.com/ykdojo/claude-code-tips

## 1. Terminal vs VS Code vs Desktop vs Cowork

Terminal 版本通常是最進階的——Claude Code 就是從這裡開始的，我覺得它投入的開發時間最多，所以功能也最豐富。有些人比較喜歡 VS Code 擴充套件，技術背景較少的使用者可能會偏好 Cowork。但如果你能用 terminal，我建議從那裡開始。

## 2. 安裝特定版本

Terminal 版本有 npm 和 native binary（原生二進位檔）兩種安裝方式。Native binary 運作得不錯，但我個人建議安裝 2.1.19 版而不是最新版，因為新版可能會有 bug（或者選一個你喜歡的版本）。你可以這樣安裝特定版本：

```bash
curl -fsSL https://claude.ai/install.sh | bash -s 2.1.19
```

Windows PowerShell 上：

```powershell
& ([scriptblock]::Create((irm https://claude.ai/install.ps1))) 2.1.19
```

你可以用 `claude --version` 來確認安裝結果。

## 3. 備份重要檔案並使用版本控制

不要成為[那個人](https://www.reddit.com/r/ClaudeAI/comments/1pgxckk/claude_cli_deleted_my_entire_home_directory_wiped/)——整個家目錄都被刪掉了。開始之前先備份所有重要的東西，並對你的專案使用版本控制（Git）。Claude Code 可能會犯錯，有了版本控制就代表你隨時可以回滾。

## 4. 學會好好測試輸出結果

Claude Code 和 AI 整體的問題在於，它們可能會引入不容易察覺的 bug。所以一定要好好測試輸出結果，這樣才不會累積一堆 bug。你甚至可以讓 Claude Code 測試自己的程式碼——比如讓它寫測試。只要確保測試看起來是合理的就好。

## 5. 把重複的指令放進 CLAUDE.md

如果你發現自己一直在對 Claude Code 說同樣的事情，就把那些指令放到 CLAUDE.md 檔案裡。你可以直接叫 Claude Code 幫你做——放在專案資料夾（`./CLAUDE.md`）裡是專案專用的指令，或者放在全域位置（`~/.claude/CLAUDE.md`）就是到處都適用的。它應該能找到正確的檔案並幫你編輯。

如果 Claude Code 沒有一致地遵循某個指令，另一個選擇是設定 [hook](https://docs.anthropic.com/en/docs/claude-code/hooks)。例如，如果你想讓它永遠使用 `python3.12` 而不是 `python3`，你可以建立一個 hook 來阻止它執行 `python3`，並告訴它改用 `python3.12`。

## 6. 設定瀏覽器整合

如果你需要 Claude Code 跟網頁互動，我推薦以下兩個選項：

- **Playwright MCP** - 大多數任務表現比較好。用這個指令安裝：`claude mcp add -s user playwright npx @playwright/mcp@latest`
- **Claude in Chrome** - 用 `/chrome` 切換。當你需要使用自己瀏覽器設定檔的登入狀態時很好用。

如果你用 Claude in Chrome，我建議在你的 CLAUDE.md 加入以下內容來讓它更穩定：

```markdown
# Claude for Chrome

- Use `read_page` to get element refs from the accessibility tree
- Use `find` to locate elements by description
- Click/interact using `ref`, not coordinates
- NEVER take screenshots unless explicitly requested by the user
```

## 7. 學會快速審查輸出

我個人用 GitHub Desktop 來做這件事。它有很好的 diff 檢視，可以輕鬆看到 Claude Code 到底改了什麼。你也可以讓 Claude Code 建立一個 draft PR（草稿拉取請求），在那邊審查後再轉成正式的 PR。

## 8. 研究、規劃、執行、測試

1. **研究** - 先花夠多時間理解問題。建立領域知識，這樣你才能有效引導 Claude Code。
2. **規劃** - 在寫程式碼之前，讓 Claude Code 先想出一個計畫。你可以用 plan mode（`/plan` 或 Shift+Tab）來做這件事。
3. **執行** - 寫程式碼。
4. **測試** - 確保一切真的能動。

## 9. 保持每段對話簡短

當你開始一段新的 Claude Code 對話時，它的表現是最好的，因為沒有之前上下文帶來的複雜度。隨著你跟它聊越久，context 越來越長，效能通常會下降。

所以每個新主題就開一段新對話，或者每當效能開始下降時就換一段。很多短而專注的對話比一段很長的對話好得多。

## 10. 學會同時處理多個 session

當你對 Claude Code 比較熟練後，試試同時在不同的 terminal 分頁跑兩到三個 session。我的方法是我稱之為「瀑布式」的做法——每當我開始一個新任務，我就在右邊開一個新分頁。然後從左到右掃過去，從最舊的任務到最新的。

我建議同時最多專注在三到四個任務上。超過這個數量就很難追蹤每個任務的進度了。

## 11.（加碼）用 Git worktree 來平行處理不同分支

如果你在同一個專案裡同時做好幾件事，又不想讓它們互相衝突，Git worktree 是個很好的方式。你可以直接叫 Claude Code 建立一個 git worktree 然後在那邊工作——不用擔心具體的語法。

基本的概念就是你可以在不同的目錄裡處理不同的 branch。

### 什麼是 git worktree？

Git worktree 就像是任何其他的 git branch，但有一個專門指定給它的新目錄。

所以如果你正在處理，比方說，main branch 和 feature-branch-1，那不用 git worktree 的話，你一次只能處理一個，因為你的專案資料夾一次只能設定在一個 branch 上。

但是有了 git worktree，你可以繼續在原本的專案資料夾裡處理 main branch（或任何其他 branch），同時在一個新的資料夾裡處理 feature-branch-1。

![Git worktrees 圖示：在不同目錄平行處理不同分支](https://raw.githubusercontent.com/ykdojo/claude-code-tips/main/assets/git-worktrees.png)

---

如果想看更完整的 25 個技巧，可以看我另一篇 Reddit 貼文：https://www.reddit.com/r/ClaudeAI/comments/1qgccgs/25_claude_code_tips_from_11_months_of_intense_use/
