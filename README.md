# 🌸 SoulSpy — Multi-Agent D2C Competitive Intelligence System

<div align="center">

![SoulSpy Banner](https://img.shields.io/badge/SoulSpy-D2C%20Intelligence-ff6b9d?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyQzYuNDggMiAyIDYuNDggMiAxMnM0LjQ4IDEwIDEwIDEwIDEwLTQuNDggMTAtMTBTMTcuNTIgMiAxMiAyem0tMiAxNWwtNS01IDEuNDEtMS40MUwxMCAxNC4xN2w3LjU5LTcuNTlMMTkgOGwtOSA5eiIvPjwvc3ZnPg==)
![n8n](https://img.shields.io/badge/Built%20with-n8n-EA4B71?style=for-the-badge&logo=n8n)
![Gemini](https://img.shields.io/badge/AI-Gemini%201.5%20Flash-4285F4?style=for-the-badge&logo=google)
![Apify](https://img.shields.io/badge/Scraping-Apify-00C4CC?style=for-the-badge)
![Google Sheets](https://img.shields.io/badge/Dashboard-Google%20Sheets-34A853?style=for-the-badge&logo=googlesheets)

**An autonomous 3-agent pipeline that scrapes Amazon reviews, runs competitive analysis, and delivers weekly brand intelligence for D2C skincare brands — with zero manual effort.**

[📺 Watch Demo](#demo) · [🚀 Quick Start](#quick-start) · [🏗️ Architecture](#architecture) · [📊 Sample Output](#sample-output)

</div>

---

## 📺 Demo

<<<<<<< HEAD
https://github.com/user-attachments/assets/356c6cbe-2482-4e41-a646-5a8e3c632415
=======
> 🎬 **Video walkthrough coming soon** — showing full pipeline run on Soulflower vs WOW vs Mamaearth

<!-- 
  ============================================================
  REPLACE THIS SECTION WITH YOUR LOOM / YOUTUBE VIDEO LINK
  ============================================================
  
  Option 1 — Loom:
  [![Watch Demo](https://cdn.loom.com/sessions/thumbnails/YOUR_LOOM_ID-with-play.gif)](https://www.loom.com/share/YOUR_LOOM_ID)
  

  ============================================================

https://github.com/user-attachments/assets/356c6cbe-2482-4e41-a646-5a8e3c632415


-->
>>>>>>> 237c51d46c89054a0474b082b189aa4a755ffaa4

---

## 🎯 What Is SoulSpy?

SoulSpy is a fully autonomous competitive intelligence system built for D2C skincare brands. It monitors **Soulflower vs WOW Skin Science vs Mamaearth** across Amazon India — scraping real customer reviews weekly, running multi-layer analysis, and delivering actionable brand strategy — all without human intervention.

### The Business Problem It Solves

Manual brand monitoring for a D2C company typically involves:
- Manually reading hundreds of competitor reviews weekly
- Spreadsheet-based sentiment tracking
- Subjective, opinion-based strategy decisions
- ~6 hours/week of analyst time

**SoulSpy automates all of this in under 5 minutes.**

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    SOULSPY PIPELINE                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ⏰ Schedule Trigger (Every Sunday 9AM)                     │
│         │                                                   │
│         ▼                                                   │
│  🕷️  APIFY — Amazon Reviews Scraper                        │
│     Scrapes 6 products × 30 reviews = 180 reviews          │
│     Brands: Soulflower | WOW | Mamaearth                   │
│     Categories: Hair Oil | Shampoo                         │
│         │                                                   │
│         ▼                                                   │
│  🧹 CODE NODE 1 — Data Cleaning (JavaScript)               │
│     • Deduplication                                         │
│     • Brand mapping via Product_Id                         │
│     • Rating normalization                                  │
│     • Verified purchase tagging                            │
│         │                                                   │
│         ▼                                                   │
│  🗂️  CODE NODE 2 — Categorization (JavaScript)             │
│     • Groups by Brand + Category                           │
│     • Soulflower_Hair Oil | Soulflower_Shampoo             │
│     • WOW_Hair Oil | WOW_Shampoo                           │
│     • Mamaearth_Hair Oil | Mamaearth_Shampoo               │
│         │                                                   │
│         ▼                                                   │
│  🤖 AGENT 1 — Competitive Gap Agent (Gemini 1.5 Flash)     │
│     Reads raw reviews → generates:                         │
│     • Soulflower strengths & vulnerabilities               │
│     • Competitor weaknesses                                │
│     • Sentiment per product category                       │
│     • Top complaints & praises                             │
│         │                                                   │
│         ▼                                                   │
│  🤖 AGENT 2 — Strategy Agent (Gemini 1.5 Flash)            │
│     Reads gap analysis → generates:                        │
│     • Product improvement recommendations                  │
│     • Marketing angles vs competitors                      │
│     • Urgent fixes                                         │
│     • Weekly priority action                               │
│         │                                                   │
│         ▼                                                   │
│  🔀 IF NODE — Confidence Gate                              │
│     confidence_score >= 7 → proceed                        │
│     confidence_score < 7  → flag for human review         │
│         │                          │                        │
│         ▼                          ▼                        │
│  🤖 AGENT 3 — Reporting Agent   📋 Flagged Sheet           │
│     Executive summary                                       │
│     Brand health score (0-10)                              │
│     Competitive position                                    │
│         │                                                   │
│         ▼                                                   │
│  📊 GOOGLE SHEETS DASHBOARD (4 tabs)                       │
│     Weekly Feed | Sentiment Tracker                        │
│     Strategy Log | Flagged for Review                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 🤖 The 3-Agent System

Each agent has a **single responsibility** and passes structured JSON to the next — mirroring production multi-agent architectures like CrewAI and LangGraph.

| Agent | Role | Input | Output |
|---|---|---|---|
| **Agent 1 — Gap Analysis** | Reads raw reviews, extracts competitive intelligence | 180 categorized reviews | Strengths, vulnerabilities, sentiment, complaints |
| **Agent 2 — Strategy** | Converts intelligence into brand strategy | Agent 1 JSON output | Product improvements, marketing angles, urgent fixes |
| **Agent 3 — Reporting** | Formats everything for senior management | Agent 2 JSON output | Executive summary, brand health score, top 3 actions |

### Human-in-the-Loop Design
Agent 2 returns a `confidence_score (0-10)`. If score < 7, the pipeline routes output to a **"Flagged for Review"** tab instead of auto-publishing — ensuring a human validates low-confidence insights before they reach decision-makers.

---

## 🛠️ Tech Stack

| Component | Tool | Purpose |
|---|---|---|
| Workflow Orchestration | n8n (self-hosted, Docker) | Pipeline engine |
| Review Scraping | Apify — Amazon Reviews Scraper | Data ingestion |
| AI Reasoning | Google Gemini 1.5 Flash | All 3 agents |
| Data Processing | JavaScript (n8n Code nodes) | Cleaning & categorization |
| Dashboard | Google Sheets | Output & visualization |

**Cost:** ~$0 (Apify free tier + Gemini free tier + n8n self-hosted)

---

## 📊 Sample Output

### Agent 1 — Competitive Gap Analysis
```json
{
  "soulflower_strengths": [
    "Effective for hair growth, particularly the Rosemary Hair Oil",
    "Praised for natural ingredients and refreshing fragrance",
    "Good value for money, effective against dandruff"
  ],
  "soulflower_vulnerabilities": [
    "Inconsistent shampoo performance with reports of severe hair fall",
    "Shampoo can be drying for certain hair types",
    "Product effectiveness sometimes seen as over-hyped"
  ],
  "highest_threat_competitor": "WOW — strong brand loyalty, positive reviews focused on results",
  "soulflower_hair_oil_sentiment": "Positive",
  "soulflower_shampoo_sentiment": "Neutral",
  "data_confidence": 7
}
```

### Agent 2 — Strategy Recommendations
```json
{
  "product_improvements": [
    "Reformulate shampoo with shea butter/aloe vera to mitigate drying effect",
    "Launch new shampoo variant for Oily & Dandruff-Prone Scalps",
    "Introduce Hair Type Quiz on website to manage expectations"
  ],
  "urgent_fixes": [
    "Update shampoo page with clear hair type disclaimer immediately",
    "Proactively contact users reporting hair fall — offer refund + Rosemary Oil"
  ],
  "weekly_priority": "Launch damage control initiative: update disclaimer + begin customer outreach",
  "confidence_score": 9
}
```

### Agent 3 — Executive Report
```json
{
  "executive_summary": "Urgent shampoo damage control required. Rosemary Hair Oil performing strongly. WOW identified as highest competitive threat. Key actions: product page disclaimer, customer outreach, shampoo reformulation roadmap.",
  "brand_health_score": 4,
  "top_3_actions": [
    "Update shampoo page with usage disclaimer immediately",
    "Proactively contact users who reported severe hair fall",
    "Leverage competitor packaging failures in marketing"
  ],
  "competitive_position": "Challenger"
}
```

---

## 🚀 Quick Start

### Prerequisites
- Docker installed
- n8n running locally (`localhost:5678`)
- Apify account (free tier)
- Google Gemini API key (free)
- Google account (for Sheets)

### Step 1 — Clone the repo
```bash
git clone https://github.com/YOUR_USERNAME/soulspy.git
cd soulspy
```

### Step 2 — Import workflow into n8n
```
1. Open localhost:5678
2. Go to Workflows → Import
3. Upload: workflows/soulspy_main.json
```

### Step 3 — Add credentials in n8n
```
Settings → Credentials → Add:
  • Apify API Token
  • Google Gemini API Key  
  • Google Sheets OAuth
```

### Step 4 — Update ASINs (optional)
In `Code Node 1`, update `URL_BRAND_MAP` with your target product ASINs.

### Step 5 — Set up Google Sheet
```
1. Create new Google Sheet: "SoulSpy Dashboard"
2. Add 4 tabs: Weekly Feed | Sentiment Tracker | Strategy Log | Flagged
3. Add headers as per /docs/sheet_headers.md
4. Paste Sheet URL into all Google Sheets nodes in n8n
```

### Step 6 — Run it
```
Hit "Execute Workflow" in n8n
Watch data populate in Google Sheets in ~2 minutes
```

---

## 📁 Repository Structure

```
SoulSpy/
├── README.md
├── workflows/
│   └── soulspy_main.json        ← import this into n8n
├── docs/
│   ├── architecture.png         ← pipeline diagram
│   └── sheet_headers.md         ← exact headers for Google Sheets
├── sample_output/
│   ├── agent1_output.json       ← sample gap analysis
│   ├── agent2_output.json       ← sample strategy
│   └── agent3_output.json       ← sample report
└── assets/
    └── demo.gif                 ← workflow demo recording
```

---

## 💡 Key Design Decisions

**Why n8n over Make.com?**
n8n supports native JavaScript Code nodes, giving full algorithmic control over data transformation. The visual canvas also makes the multi-agent architecture immediately understandable in a demo.

**Why Gemini over OpenAI?**
Gemini 1.5 Flash is completely free with generous rate limits — making this project zero-cost and reproducible by anyone.

**Why separate agents instead of one big prompt?**
Single-responsibility agents produce more focused, higher-quality outputs. Agent 2 (Strategy) returned `confidence_score: 9` when working from Agent 1's structured output — compared to lower confidence when working from raw reviews directly. This validates the multi-agent approach.

**Why a confidence gate?**
Production agentic systems need human oversight mechanisms. The IF node routing low-confidence outputs to a review queue demonstrates responsible AI system design — not just automation.

---

## 📈 Impact Metrics

| Metric | Before SoulSpy | After SoulSpy |
|---|---|---|
| Weekly review monitoring time | ~6 hours | ~0 hours |
| Brands monitored simultaneously | 1 | 3 |
| Products tracked | Manual | 6 (expandable) |
| Strategy generation time | Days | Minutes |
| Consistency of analysis | Variable | Standardized |

---

## 🔮 Roadmap

- [ ] Add more brands (Biotique, The Moms Co, Wow)
- [ ] Expand to Nykaa and Flipkart reviews
- [ ] Add Slack notification on urgent alerts
- [ ] Build Looker Studio dashboard on top of Sheets
- [ ] Add week-over-week trend comparison across runs
- [ ] Deploy on Railway.app for always-on execution

---



## ⚠️ Disclaimer

This project is for educational and portfolio purposes. Review data is scraped from public Amazon listings. No proprietary data is used or stored.

---

<div align="center">

**If this project helped you, give it a ⭐**

Built with 🌸 for the D2C skincare space

</div>
