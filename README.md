# Soulflower Competitor Analysis — n8n Workflow

Automated pipeline that scrapes Amazon reviews for Soulflower, WOW, and Mamaearth hair care products, runs AI-powered competitive analysis via Gemini, and writes weekly reports to Google Sheets.

## Workflow Overview

```
Schedule (every 9 days)
  → Apify: Scrape Amazon reviews (6 products × 30 reviews)
  → Data Cleaning & Deduplication
  → Categorise by Brand & Product Type
  → Gemini: Gap Analyst      → Parser1 ──┬→ Gemini: Strategist → Parser2 ──┬→ Gemini: Executive Report → Parser3 → Sheet (Executive)
                                          └→ Sheet (Sentiment)               └→ Sheet (Strategy)
```

## Google Sheets Output

3 sheets inside one Spreadsheet:
| Sheet | What it captures |
|-------|-----------------|
| Sheet 1 (gid=0) | Executive summary, brand health score, top 3 actions |
| Sheet 2 (gid=311844997) | Oil/shampoo sentiment, top praise/complaint, highest threat |
| Sheet 3 (gid=1549957976) | Weekly priority, urgent fixes, marketing angles |

---

## Local Development

### Prerequisites
- Docker & Docker Compose
- Git

### Setup

```bash
# 1. Clone the repo
git clone <your-repo-url>
cd soulflower-n8n

# 2. Copy env template and fill in your values
cp .env.example .env
# Edit .env with your actual values

# 3. Start n8n + Postgres
docker compose up -d

# 4. Open n8n
open http://localhost:5678
```

### Import the Workflow

1. Log into n8n (`admin` / your password)
2. Go to **Workflows → Import from file**
3. Select `workflows/soulflower_analysis.json`
4. Re-link credentials (see below)

---

## Credentials Setup (do this after import)

The workflow JSON uses placeholder credential IDs. After importing, re-link each one:

| Credential | n8n Type | Where to get the key |
|-----------|----------|---------------------|
| Apify account | Apify API | [Apify Console → Settings → API tokens](https://console.apify.com/) |
| Google Gemini(PaLM) Api account | Google Gemini(PaLM) API | [Google AI Studio → Get API key](https://aistudio.google.com/) |
| Google Sheets account | Google Sheets OAuth2 API | Connect via OAuth in n8n (no key to copy) |

### Set the Google Sheets Variable

In n8n: **Settings → Variables → Add Variable**
- Name: `GOOGLE_SHEETS_DOC_ID`
- Value: `1PM60bjFNQp1oUBmBZumK9fpYXEXDBWUDqmLBn7RWLvg` ← your actual Sheets doc ID

---

## Deploy to Railway

### One-time Setup

1. Push this repo to GitHub
2. Go to [railway.app](https://railway.app) → **New Project → Deploy from GitHub**
3. Select this repo
4. Add a **PostgreSQL** plugin (Railway will inject `DATABASE_URL`)
5. Set the following **environment variables** in Railway dashboard:

```
N8N_ENCRYPTION_KEY         = <random 32-char string>
N8N_BASIC_AUTH_ACTIVE      = true
N8N_BASIC_AUTH_USER        = admin
N8N_BASIC_AUTH_PASSWORD    = <strong password>
DB_TYPE                    = postgresdb
DB_POSTGRESDB_HOST         = <from Railway Postgres plugin>
DB_POSTGRESDB_PORT         = 5432
DB_POSTGRESDB_DATABASE     = railway
DB_POSTGRESDB_USER         = postgres
DB_POSTGRESDB_PASSWORD     = <from Railway Postgres plugin>
N8N_VARIABLES_GOOGLE_SHEETS_DOC_ID = <your sheets doc id>
WEBHOOK_URL                = https://<your-railway-domain>/
GENERIC_TIMEZONE           = Asia/Kolkata
```

6. Deploy → Railway builds the Docker image and starts n8n
7. Open your Railway URL, log in, import the workflow, set up credentials

### Railway Tips
- Railway auto-assigns a domain like `your-app.up.railway.app` — set this as `WEBHOOK_URL`
- For Google OAuth credentials, you'll need to add the Railway URL to your Google Cloud Console OAuth redirect URIs

---

## What's NOT in this repo (intentionally)

| Secret | Where it lives |
|--------|---------------|
| Apify API token | n8n Credentials (encrypted in DB) |
| Google Gemini API key | n8n Credentials (encrypted in DB) |
| Google OAuth tokens | n8n Credentials (encrypted in DB) |
| `.env` file | Your local machine only — never committed |
| `client_secret_*.json` | Never committed (in `.gitignore`) |
