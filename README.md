# creator-contest-pipeline
AI-powered creator contest automation for Web3 projects — Notion + n8n + OpenAI
 Creator Contest Pipeline
 AI-powered creator contest automation for Web3 projects


 What Is This?

A fully automated creator contest management pipeline built for Web3 projects and bounty campaigns.

Instead of manually tracking submissions, judging creators by gut feel, and rebuilding spreadsheets for every contest  this pipeline does everything automatically.

Creators submit a link. AI scores them. A live leaderboard updates every 30 minutes. Zero manual work.**



The Problem It Solves

Web3 projects run creator contests constantly as their #1 community growth strategy. But behind the scenes, teams are:

-  Manually checking Twitter & TikTok for every submission
-  Scoring creators inconsistently, causing community backlash
- Running no live leaderboard, so creators disengage mid-contest
-  Rebuilding the same spreadsheet for every new campaign

This pipeline eliminates all of that permanently.

---

 What It Does

| Feature | Description |
|---|---|
|  **Contest Entry Form** | Creators submit name, platform, link and engagement stats in one form |
|  **AI Scoring** | OpenAI scores every submission on 5 criteria automatically |
|  **Live Leaderboard** | Creators ranked Gold / Silver / Bronze, updated every 30 minutes |
|  **Gold Creators View** | Dedicated view showing only top performers |
|  **Platform Split** | Separate views for Twitter vs TikTok performance |
|  **Performance Overview** | % performing well, tier distribution, average scores |
|  **Instant Alerts** | Slack notification when a Gold-tier creator enters |

---

 How The AI Scores Creators

Every submission is evaluated on 5 criteria by OpenAI GPT-4.1-mini:

```
Engagement Score  (30%) — likes + shares + replies vs views
Sentiment Score   (20%) — comment tone & community reception  
Originality Score (20%) — creative hook & unique content angle
Reach Score       (15%) — raw views & impression volume
Brand Fit Score   (15%) — alignment with project values
```

**Composite Score = weighted average of all 5 criteria**

| Tier | Score | Badge |
|---|---|---|
| Gold | 80–100 | 
| Silver | 60–79 | 
| Bronze | 40–59 | 
| Unranked | Below 40 |

---

Tech Stack

| Tool | Role |
|---|---|
| **Notion** | Database, leaderboard, contest entry form, dashboard |
| **n8n** | Automation engine — polls Notion, triggers scoring, updates records |
| **OpenAI GPT-4.1-mini** | AI scoring engine |
| **Slack** | Gold tier creator alerts (optional) |

---

 Repository Structure

```
creator-contest-pipeline/
│
├── n8n-workflow-no-api.json      # Import this directly into n8n
├── claude-scoring-prompt.txt     # AI scoring prompt template + docs
├── notion-setup-guide.txt        # Full 10-step Notion setup guide
├── README.md                     # You are here
│
└── assets/
    └── screenshots/
        ├── leaderboard.png       # Live leaderboard view
        ├── contest-entry.png     # Creator submission form
        ├── n8n-workflow.png      # Full n8n pipeline
        └── dashboard.png         # Contest dashboard
```

 Quick Start

Prerequisites
- [Notion](https://notion.so) account (free)
- [n8n](https://n8n.io) account (free cloud plan works)
- [OpenAI](https://platform.openai.com) API key (~$5 to start)
- Slack webhook URL (optional, for Gold alerts)

 Setup Steps

**1. Set up Notion database**
Follow the step-by-step guide in `notion-setup-guide.txt`

Your database needs these key properties:
```
Creator Name    → Title
Platform        → Select (Twitter, TikTok)
Content URL     → URL
Caption         → Text
Likes           → Number
Reposts         → Number
Replies         → Number
Views           → Number
Follower Count  → Number
Status          → Select (Pending, Processed, Error)
AI Score        → Number
Tier            → Select (Gold, Silver, Bronze, Unranked)
Engagement Score → Number
Sentiment Score  → Number
Originality Score → Number
Reach Score      → Number
Brand Fit Score  → Number
Performing Well  → Checkbox
AI Notes        → Text
```

**2. Import n8n workflow**
- Open n8n → click `...` → Import from file
- Upload `n8n-workflow-no-api.json`
- Replace these placeholders:

```
YOUR_NOTION_DATABASE_ID  → your 32-char database ID
YOUR_OPENAI_API_KEY      → from platform.openai.com
YOUR_SLACK_WEBHOOK_URL   → from api.slack.com (optional)
```

**3. Connect Notion to n8n**
- Go to notion.so/my-integrations
- Create integration named "Contest Pipeline n8n"
- Copy the Internal Integration Secret
- Add as Notion credential in n8n
- Connect integration to your database in Notion

**4. Test the pipeline**
- Add a test submission to your Notion database
- Set Status to "Pending"
- Click "Execute workflow" in n8n
- Check Notion — scores should appear within seconds 

**5. Publish**
- Click "Publish" in n8n to activate automatic 30-minute schedule

---

 How The Pipeline Works

```
1. SUBMIT    Creator fills out Notion form with their link + metrics
     ↓
2. TRIGGER   n8n polls Notion every 30 minutes for Pending submissions
     ↓
3. FILTER    Only valid submissions with a content URL pass through
     ↓
4. EXTRACT   All fields pulled from the Notion row
     ↓
5. PROMPT    Scoring prompt built with creator data
     ↓
6. SCORE     OpenAI evaluates all 5 criteria and returns JSON scores
     ↓
7. PARSE     AI response parsed into individual score fields
     ↓
8. UPDATE    Notion row updated with scores, tier, and status
     ↓
9. ALERT     If Gold tier → Slack notification fired (optional)
```

---

 Current Limitations (Demo Version)

This is a demo version with manual metric entry. The full production version will include:

- **Twitter API** — auto-fetch engagement metrics (requires $100/month Basic plan)
- **TikTok API** — auto-fetch video metrics (requires app approval, 2–4 weeks)
- **Slack alerts** — real-time Gold creator notifications
- **Cumulative leaderboard** — tracks creator scores across multiple submissions per week

**Why manual entry for now?**
Twitter API costs $100/month and TikTok API requires weeks of approval. For the demo and early clients, creators self-report their metrics via the form. The AI scoring, automation, and leaderboard all work identically — only the data source changes in production.

---

  Roadmap

- [x] Notion database setup
- [x] n8n automation workflow
- [x] OpenAI scoring engine
- [x] Live leaderboard
- [x] Gold creators view
- [x] Platform split view
- [x] Contest entry form
- [ ] Twitter API auto-fetch
- [ ] TikTok API auto-fetch
- [ ] Slack Gold alerts
- [ ] Cumulative multi-submission leaderboard
- [ ] Email digest reports
- [ ] Public-facing leaderboard page

---

 Contributing

Pull requests welcome! If you have suggestions for improving the AI scoring prompt, adding new criteria, or extending the pipeline  open an issue or PR.

 License

MIT License use freely, attribution appreciated.

---

 Author

Built by **Damilola Sodiq Ajadi**

- Twitter: @damexyThe
- Telegram: @just_That_guyf
- Email: ajadisodiq0062@gmail.com
