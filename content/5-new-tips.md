# 5 個新的 Claude Code 技巧

之前我發了 [32 個 Claude Code 技巧：從基礎到進階](https://agenticcoding.substack.com/p/32-claude-code-tips-from-basics-to)。這裡再補充 5 個新技巧。

## 1. `/copy` 命令

把 Claude 的輸出從 terminal 拿出來最簡單的方式。只要打 `/copy`，它就會把 Claude 的最後一個回應以 markdown 格式複製到你的剪貼簿。

## 2. `/fork` 和 `--fork-session`

Claude Code 現在有內建的對話分叉功能：

- `/fork` - 在對話中分叉
- `--fork-session` - 搭配 `--resume` 或 `--continue` 使用（例如 `claude -c --fork-session`）

因為 `--fork-session` 沒有簡短形式，我建了一個 shell function 來用 `--fs` 當快捷方式。[可以在這裡看到](https://github.com/ykdojo/claude-code-tips?tab=readme-ov-file#tip-23-clonefork-and-half-clone-conversations)。

## 3. 用 plan mode 做 context handoff（上下文交接）

用 `/plan` 或 Shift+Tab 進入 plan mode。叫 Claude 收集下一個 agent 需要的所有 context：

> I just enabled plan mode. Bring over all of the context that you need for the next agent. The next agent will not have any other context, so you'll need to be pretty comprehensive.

完成後，選 Option 1（「Yes, clear context and auto-accept edits」）來重新開始，只保留計畫。新的 Claude 實例只看到計畫，沒有舊對話的包袱。

## 4. 定期檢視 CLAUDE.md

你的 CLAUDE.md 檔案會隨時間過時。幾週前合理的指令可能已經不再適用。我建了一個 `review-claudemd` skill 來分析你最近的對話並建議改善。[可以在這裡看看](https://github.com/ykdojo/claude-code-tips/tree/main/skills/review-claudemd)。

## 5. 用 Parakeet 做語音轉文字

我一直在用語音轉文字來跟 Claude Code 對話，而不是打字。我剛在 [Super Voice Assistant](https://github.com/ykdojo/super-voice-assistant)（開源）裡加了 Parakeet 的支援，它非常快——Parakeet v2 的運行速度大約是即時的 110 倍，字錯率只有 1.69%。精準度對 Claude Code 來說綽綽有餘。
