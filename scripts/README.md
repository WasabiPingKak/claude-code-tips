# Claude Code Scripts

## context-bar.sh

一個兩行的狀態列 script，用於 Claude Code，會顯示 model、目錄、git branch、未 commit 的檔案數、跟 origin 的同步狀態、context 使用量，以及你的上一條訊息。

**範例輸出：**
```
Opus 4.5 | 📁claude-code-tips | 🔀main (scripts/context-bar.sh uncommitted, synced 12m ago) | ██░░░░░░░░ 18% of 200k tokens
💬 This is good. I don't think we need to change the documentation as long as we don't say that the default color is orange el...
```

### 安裝

1. 把 script 複製到你的 Claude scripts 目錄：
   ```bash
   mkdir -p ~/.claude/scripts
   cp context-bar.sh ~/.claude/scripts/
   chmod +x ~/.claude/scripts/context-bar.sh
   ```

2. 更新你的 `~/.claude/settings.json`：
   ```json
   {
     "statusLine": {
       "type": "command",
       "command": "~/.claude/scripts/context-bar.sh"
     }
   }
   ```

搞定！

### 顏色主題

這個 script 支援選用顏色主題來設定 model 名稱和進度條的顏色。編輯 script 頂部的 `COLOR` 變數：

```bash
# Color theme: gray, orange, blue, teal, green, lavender, rose, gold, slate, cyan
COLOR="orange"
```

執行 `bash scripts/color-preview.sh` 預覽所有選項：

![Color preview options](color-preview.png)

### 需求

- `jq`（用來解析 JSON）
- `bash`
- `git`（選用，用來顯示 branch）
- Claude Code 2.0.65+（確認可用；更舊的版本可能沒有所需的 JSON 欄位——舊版本請查看更早的 commit）

### 運作原理

Claude Code 會透過 stdin 以 JSON 格式把 session metadata 傳給狀態列指令，包含：
- `model.display_name` - Model 名稱
- `cwd` - 當前工作目錄
- `context_window.total_input_tokens` - 已使用的 input token 總數
- `context_window.total_output_tokens` - 已使用的 output token 總數
- `context_window.context_window_size` - 最大 context window 大小
- `transcript_path` - Session transcript JSONL 檔案的路徑

這個 script 用這些 JSON 欄位來計算 context 使用量（input + output tokens），顯示 context window 的使用百分比。用 `/context` 可以看精確的 token 明細。
