---
name: half-clone
description: Clone the later half of the current conversation, discarding earlier context to reduce token usage while preserving recent work.
---

複製當前對話的後半段，丟棄前半段的 context，藉此減少 token 用量，同時保留最近的工作進度。

步驟：
1. 取得當前的 session ID 和專案路徑：`tail -1 ~/.claude/history.jsonl | jq -r '[.sessionId, .project] | @tsv'`
2. 用 bash 找到 half-clone-conversation.sh：`find ~/.claude -name "half-clone-conversation.sh" 2>/dev/null | sort -V | tail -1`
   - 不管是透過 plugin 安裝還是手動 symlink，這樣都找得到
   - 用 version sort 確保有多個版本時選最新的
3. 預覽對話以確認 session ID：`<script-path> --preview <session-id> <project-path>`
   - 檢查第一條和最後一條訊息是否跟當前對話一致
4. 執行 clone：`<script-path> <session-id> <project-path>`
   - 永遠從 history entry 拿專案路徑，不要用當前工作目錄
5. 告訴使用者可以用 `claude -r` 來存取 half-clone 後的對話，找標記為 `[HALF-CLONE <timestamp>]` 的那個（例如 `[HALF-CLONE Jan 7 14:30]`）。script 會自動在 clone 檔案的結尾加上對原始對話的參照。
