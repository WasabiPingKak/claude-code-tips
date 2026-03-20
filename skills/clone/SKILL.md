---
name: clone
description: Clone the current conversation so the user can branch off and try a different approach.
---

複製當前對話，讓使用者可以從這裡分支出去嘗試不同的方法。

步驟：
1. 取得當前的 session ID 和專案路徑：`tail -1 ~/.claude/history.jsonl | jq -r '[.sessionId, .project] | @tsv'`
2. 用 bash 找到 clone-conversation.sh：`find ~/.claude -name "clone-conversation.sh" 2>/dev/null | sort -V | tail -1`
   - 不管是透過 plugin 安裝還是手動 symlink，這樣都找得到
   - 用 version sort 確保有多個版本時選最新的
3. 執行：`<script-path> <session-id> <project-path>`
   - 永遠從 history entry 拿專案路徑，不要用當前工作目錄
4. 告訴使用者可以用 `claude -r` 來存取 clone 後的對話，找標記為 `[CLONED <timestamp>]` 的那個（例如 `[CLONED Jan 7 14:30]`）
