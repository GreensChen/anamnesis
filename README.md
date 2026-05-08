# Anamnesis

> ἀνάμνησις — recollection, the bringing back to mind of forgotten knowledge (Plato).

個人 Obsidian 知識庫的 capture / process / chat / quiz 流程。Telegram bot
做即時 capture（影片、文章、截圖、文字）、Gemini 做 AI 摘要與對話、自我演化
的 tag vocabulary 維持 vault 的長期清晰。

姊妹專案：[Pharos](https://github.com/GreensChen/yt2epub) — YouTube → 雙語繁中
.kepub.epub → Kobo 慢讀。

## 你會用到的指令（Telegram）

| 指令 | 行為 |
|---|---|
| `/review` | 從 Dropbox `/Kobo Highlights/` 抓未 process 的 highlight、一條一條卡片化。回覆文字 reaction 自動寫入 `0 Inbox/` |
| `/skipall` | 把所有 pending 標記為已處理（清歷史） |
| `/quiz` | Active recall：從你某本書 / 訪談的 overview + highlights 出 3 選 1 題、答完存 `2 Atomic Notes/Quizzes/` |
| `/ask <問題>` | 用整個 vault 當 context 對話、`/endchat` 結束時 AI 寫摘要、整段存 `2 Atomic Notes/Conversations/` |
| 直接貼 YouTube URL | Gemini 看影片 → `1 Sources/Videos/<title>.md` |
| 直接貼其他 URL | 抓網頁 + 摘要 → `1 Sources/Articles/<title>.md` |
| 貼 1-3 張截圖 | OCR + 內容拼接 → `1 Sources/Articles/<title>.md` |
| 貼 ≥ 500 字長文 | 摘要當文章 → `1 Sources/Articles/` |
| 貼 < 500 字短文 | 原樣存 spark → `0 Inbox/spark-<ts>.md` |

## Mac 端 script

| Script | 用途 |
|---|---|
| `generate_book_overviews.py` | 對 vault Highlights / Transcripts 生成 Books / Interviews overview |
| `sync_to_obsidian.py` | yt2epub 產的 `_data.json` → vault Transcripts |
| `bootstrap_vocabulary.py` | 一次性對 vault 所有檔生 topical tag |
| `consolidate_vocabulary.py` | AI 找 synonym / 過細 tag 自動 merge |

## Vault 結構（user 端）

```
~/Dropbox/Greens Obsidian/
├── 0 Inbox/                # Telegram capture spark
├── 1 Sources/
│   ├── Books/              # 書籍 overview（type: book）
│   ├── Interviews/         # 訪談 overview（type: interview）
│   ├── Transcripts/        # yt2epub 完整逐字稿（type: transcript）
│   ├── Highlights/         # kobo-highlight 推來的重點（read-only）
│   ├── Articles/           # 文章 / 截圖 / 長文（type: article / post）
│   └── Videos/             # YouTube 摘要（type: video）
├── 2 Atomic Notes/
│   ├── Quizzes/
│   ├── Conversations/      # /ask 對話 log
│   └── Vocabulary Changelog.md  # AI 自動 merge tag 的紀錄
├── 3 MOCs/
├── 4 Daily/
├── 9 Attachments/
└── .vocabulary.json        # 自演化的 canonical tag 清單
```

## 部署

```bash
# Mac → server
export SERVER_IP=your.server.ip
./server/deploy.sh

# server 上
sudo /home/yt2epub/anamnesis/server/install_services.sh
```

## License

MIT
