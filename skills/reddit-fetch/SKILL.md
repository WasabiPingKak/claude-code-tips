---
name: reddit-fetch
description: Fetch content from Reddit using Gemini CLI or curl JSON API fallback. Use when accessing Reddit URLs, researching topics on Reddit, or when Reddit returns 403/blocked errors.
---

# Reddit Fetch

## 方法一：Gemini CLI（優先嘗試）

透過 tmux 使用 Gemini CLI。它可以瀏覽、摘要，並回答關於 Reddit 內容的複雜問題。

選一個唯一的 session 名稱（例如 `gemini_abc123`），整個過程中都用同一個。

### 設定

```bash
tmux new-session -d -s <session_name> -x 200 -y 50
tmux send-keys -t <session_name> 'gemini -m gemini-3-pro-preview' Enter
sleep 3  # wait for Gemini CLI to load
```

### 送出查詢並擷取輸出

```bash
tmux send-keys -t <session_name> 'Your Reddit query here' Enter
sleep 30  # wait for response (adjust as needed, up to 90s for complex searches)
tmux capture-pane -t <session_name> -p -S -500  # capture output
```

如果擷取的輸出顯示 API 錯誤（例如 quota 用完、model 不可用），就把 session 關掉，然後不帶 `-m` flag 重試（只用 `gemini`，不帶 model 參數）。這樣會 fallback 到預設 model。

### 怎麼判斷 Enter 有沒有送出

找你的查詢文字，看它是在框框裡面還是外面。

**Enter 沒有送出** - 你的查詢在框框裡面：
```
╭─────────────────────────────────────╮
│ > Your actual query text here       │
╰─────────────────────────────────────╯
```

**Enter 已經送出** - 你的查詢在框框外面，後面有活動：
```
> Your actual query text here

⠋ Our hamsters are working... (processing)

╭────────────────────────────────────────────╮
│ >   Type your message or @path/to/file     │
╰────────────────────────────────────────────╯
```

注意：空白的 prompt `Type your message or @path/to/file` 總是會出現在框框裡——這是正常的。重點是你的查詢文字是在框框裡面還是外面。

如果你的查詢在框框裡面，執行 `tmux send-keys -t <session_name> Enter` 來送出。

### 完成後清理

```bash
tmux kill-session -t <session_name>
```

### 如果 Gemini 完全失敗

如果不帶 `-m` 重試也失敗了，就改用下面的方法二。

---

## 方法二：用 curl 呼叫 Reddit JSON API（備用方案）

Reddit 的公開 JSON API 只要在任何 Reddit URL 後面加 `.json` 就能用。當 Gemini 不可用時（quota 耗盡、API 錯誤等）就用這個。

### 列出熱門/最新/排行文章

```bash
curl -s -H "User-Agent: Mozilla/5.0 (compatible; bot)" \
  "https://www.reddit.com/r/SUBREDDIT/hot.json?limit=15"
```

把 `hot` 換成 `new`、`top` 或 `rising` 看需求。如果用 `top`，加上 `&t=day`（或 `week`、`month`、`year`、`all`）。

### 抓取特定文章 + 留言

```bash
curl -s -H "User-Agent: Mozilla/5.0 (compatible; bot)" \
  "https://www.reddit.com/r/SUBREDDIT/comments/POST_ID.json?limit=20"
```

回傳的是一個 JSON 陣列：`[0]` 是文章本體，`[1]` 是留言樹。

### 在子版內搜尋

```bash
curl -s -H "User-Agent: Mozilla/5.0 (compatible; bot)" \
  "https://www.reddit.com/r/SUBREDDIT/search.json?q=QUERY&restrict_sr=on&sort=new&limit=15"
```

### 解析 JSON

用 python3 inline 來擷取你需要的資料：

```bash
curl -s -H "User-Agent: Mozilla/5.0 (compatible; bot)" \
  "https://www.reddit.com/r/SUBREDDIT/hot.json?limit=15" | python3 -c "
import json, sys
data = json.loads(sys.stdin.read())
for i, post in enumerate(data['data']['children'], 1):
    p = post['data']
    flair = p.get('link_flair_text', '') or ''
    print(f'{i}. [{flair}] {p[\"title\"]}')
    print(f'   {p[\"score\"]} pts | {p[\"num_comments\"]} comments | u/{p[\"author\"]}')
    print()
"
```

### 如果 curl 回傳空的或被擋

如果 JSON API 回傳空的回應或 HTTP 429，表示你可能被 rate-limit 了。等一下再重試，或換一個不同的 User-Agent 字串。
