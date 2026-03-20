---
name: review-claudemd
description: Review recent conversations to find improvements for CLAUDE.md files.
---

# 從對話歷史回顧 CLAUDE.md

分析最近的對話來改善全域（~/.claude/CLAUDE.md）和本地（專案）的 CLAUDE.md 檔案。

## 步驟一：找到對話歷史

專案的對話歷史在 `~/.claude/projects/`。資料夾名稱是專案路徑把斜線換成破折號。

```bash
# Find the project folder (replace / with -)
PROJECT_PATH=$(pwd | sed 's|/|-|g' | sed 's|^-||')
CONVO_DIR=~/.claude/projects/-${PROJECT_PATH}
ls -lt "$CONVO_DIR"/*.jsonl | head -20
```

## 步驟二：擷取最近的對話

把最近的 15-20 個對話（不含當前這個）擷取到暫存目錄：

```bash
SCRATCH=/tmp/claudemd-review-$(date +%s)
mkdir -p "$SCRATCH"

for f in $(ls -t "$CONVO_DIR"/*.jsonl | head -20); do
  basename=$(basename "$f" .jsonl)
  # Skip current conversation if known
  cat "$f" | jq -r '
    if .type == "user" then
      "USER: " + (.message.content // "")
    elif .type == "assistant" then
      "ASSISTANT: " + ((.message.content // []) | map(select(.type == "text") | .text) | join("\n"))
    else
      empty
    end
  ' 2>/dev/null | grep -v "^ASSISTANT: $" > "$SCRATCH/${basename}.txt"
done

ls -lhS "$SCRATCH"
```

## 步驟三：啟動 Sonnet subagent

啟動平行的 Sonnet subagent 來分析對話。每個 agent 應該讀取：
- 全域 CLAUDE.md：`~/.claude/CLAUDE.md`
- 本地 CLAUDE.md：`./CLAUDE.md`（如果存在的話）
- 一批對話檔案

給每個 agent 這個 prompt 模板：

```
Read:
1. Global CLAUDE.md: ~/.claude/CLAUDE.md
2. Local CLAUDE.md: [project]/CLAUDE.md
3. Conversations: [list of files]

Analyze the conversations against BOTH CLAUDE.md files. Find:
1. Instructions that exist but were violated (need reinforcement or rewording)
2. Patterns that should be added to LOCAL CLAUDE.md (project-specific)
3. Patterns that should be added to GLOBAL CLAUDE.md (applies everywhere)
4. Anything in either file that seems outdated or unnecessary

Be specific. Output bullet points only.
```

依對話大小分批：
- 大檔（>100KB）：每個 agent 1-2 個
- 中檔（10-100KB）：每個 agent 3-5 個
- 小檔（<10KB）：每個 agent 5-10 個

## 步驟四：彙整結果

把所有 agent 的結果整合成一份摘要，包含以下章節：

1. **被違反的指令** - 既有的規則沒被遵守（需要加強措辭）
2. **建議新增 - 本地** - 專案特定的模式
3. **建議新增 - 全域** - 適用於所有地方的模式
4. **可能過時的項目** - 可能不再相關的東西

用表格或條列呈現。問使用者要不要草擬修改。
