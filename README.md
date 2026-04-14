# 🔬 RedditLens — Market Intelligence Scraper

A Chrome Extension (Manifest V3) that transforms Reddit threads into structured JSON/CSV datasets for business intelligence, market research, and pain-point discovery.

---

## ✨ Features

| Feature | Status |
|---|---|
| Scrape post title, body, author, upvotes | ✅ MVP |
| Extract top-level comments | ✅ MVP |
| Nested replies (full tree) | ✅ MVP |
| JSON export (auto-download) | ✅ MVP |
| CSV export | ✅ MVP |
| Comment limit control (20/50/100/All) | ✅ MVP |
| New Reddit layout support | ✅ MVP |
| Old Reddit layout support | ✅ MVP |
| AI-powered pain point classification | 🗺️ Roadmap |
| Dashboard UI | 🗺️ Roadmap |
| Google Sheets integration | 🗺️ Roadmap |

---

## 🚀 Installation (Developer Mode)

### Step 1 — Add placeholder icons
The extension needs icon files. Create a folder called `icons/` inside the extension folder and add PNG images at these sizes:
- `icons/icon16.png` (16×16)
- `icons/icon48.png` (48×48)
- `icons/icon128.png` (128×128)

> **Quick option:** Copy any PNG and resize it, or generate icons at https://favicon.io

### Step 2 — Load the extension in Chrome
1. Open Chrome and navigate to `chrome://extensions`
2. Enable **Developer mode** (toggle, top-right)
3. Click **Load unpacked**
4. Select the `reddit-scraper-extension` folder
5. The RedditLens icon appears in your toolbar ✅

---

## 📖 Usage

1. Open any Reddit post (e.g. `reddit.com/r/startups/comments/...`)
2. Click the **RedditLens** extension icon
3. Adjust options:
   - **Comment Limit** — how many top-level comments to extract
   - **Include Replies** — toggle nested comment capture
   - **Export Format** — JSON or CSV
4. Click **⚡ Scrape This Thread**
5. File downloads automatically to your `Downloads` folder

---

## 📦 Output Format

### JSON
```json
{
  "title": "What's the biggest problem with SaaS onboarding?",
  "content": "I've been researching...",
  "author": "username",
  "upvotes": "2.1k",
  "subreddit": "SaaS",
  "url": "https://www.reddit.com/r/SaaS/comments/...",
  "scraped_at": "2025-01-15T10:30:00.000Z",
  "comments": [
    {
      "text": "The biggest issue is...",
      "author": "user123",
      "upvotes": "342",
      "timestamp": "2025-01-14T08:00:00Z",
      "replies": [
        {
          "text": "Totally agree, I've seen this too...",
          "author": "another_user",
          "upvotes": "45",
          "timestamp": "2025-01-14T09:15:00Z",
          "replies": []
        }
      ]
    }
  ]
}
```

### CSV
Flat format with columns: `type, depth, text, author, upvotes, timestamp`

---

## 🏗️ Architecture

```
reddit-scraper-extension/
├── manifest.json    ← Extension config (Manifest V3)
├── popup.html       ← Extension popup UI
├── popup.js         ← UI event handling + download logic
├── content.js       ← DOM scraping logic (injected into Reddit)
├── utils.js         ← Data helpers + comment classifier
├── icons/
│   ├── icon16.png
│   ├── icon48.png
│   └── icon128.png
└── README.md
```

---

## ⚙️ Permissions Used

| Permission | Reason |
|---|---|
| `activeTab` | Read the current Reddit tab |
| `scripting` | Inject content script on demand |
| `downloads` | Trigger file download |
| `host_permissions: reddit.com` | Limit scraping to Reddit only |

---

## 🗺️ Roadmap (v2+)

- [ ] AI classification layer (pain points, feature requests, praise)
- [ ] Keyword clustering across multiple posts
- [ ] Dashboard UI inside extension
- [ ] Clipboard copy (JSON/CSV)
- [ ] Google Sheets export
- [ ] Niche discovery mode (multi-post scraping)
- [ ] Sentiment trend tracking

---

## ⚠️ Notes

- This tool operates entirely client-side — no data leaves your browser.
- Reddit's DOM changes occasionally; selectors in `content.js` may need updating.
- Respects comment load state — only extracts currently visible comments.
- For large threads with "load more" comments, scroll to load them first, then scrape.

---

## 📄 License

MIT — Free for personal and commercial use.
