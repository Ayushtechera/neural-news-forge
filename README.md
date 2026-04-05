# Neural News Forge 🧠⚡

> An end-to-end autonomous AI pipeline that scrapes, summarizes, ranks and delivers a personalized daily AI news digest straight to your inbox — powered by local LLMs and RSS intelligence.

![Python](https://img.shields.io/badge/Python-3.12-blue)
![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-336791)
![Ollama](https://img.shields.io/badge/AI-Ollama%20LLaMA3.2-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

---

## 🚀 What it does

Tired of manually browsing AI news every morning? This pipeline does it all automatically:

- 📡 **Scrapes** latest AI news from OpenAI, Anthropic RSS feeds and YouTube channels
- 📄 **Fetches** full article content and video transcripts
- 🤖 **Summarizes** every article using LLaMA 3.2 running locally via Ollama
- 🎯 **Ranks** articles based on your personal interest profile
- 📧 **Delivers** a clean HTML email digest to your inbox every day

---

## 🏗️ Pipeline Architecture
- Stage 1 → RSS Feeds + YouTube Channel
		↓
- Stage 2 → Scrape & Store in PostgreSQL
		↓
- Stage 3 → Process Full Content
  (docling for articles + youtube-transcript-api)
		↓
- Stage 4 → AI Summarization
  (LLaMA 3.2 via Ollama — local, free, private)
		↓
- Stage 5 → Personalized Ranking + Email Delivery
  (Curator Agent + Gmail SMTP)

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| Language | Python 3.12 | Core pipeline |
| Database | PostgreSQL | Store articles + digests |
| ORM | SQLAlchemy | Database operations |
| AI Model | LLaMA 3.2 via Ollama | Summarization + Ranking |
| Data Validation | Pydantic | Structured AI outputs |
| RSS Parsing | feedparser | Scrape news feeds |
| Article Scraping | docling | Convert URLs to markdown |
| Transcripts | youtube-transcript-api | Fetch YouTube transcripts |
| Email | smtplib + Gmail SMTP | Send HTML digest |
| Package Manager | uv | Fast dependency management |

---

## 📁 Project Structure

neural-news-forge/
├── app/
│   ├── agent/
│   │   ├── digest_agent.py      # Summarizes each article with LLM
│   │   ├── curator_agent.py     # Ranks articles by user profile
│   │   └── email_agent.py       # Writes personalized introduction
│   ├── database/
│   │   ├── models.py            # SQLAlchemy table definitions
│   │   ├── repository.py        # All DB operations
│   │   └── connection.py        # PostgreSQL connection
│   ├── scrapers/
│   │   ├── anthropic.py         # Anthropic RSS scraper
│   │   ├── openai.py            # OpenAI RSS scraper
│   │   └── youtube.py           # YouTube RSS + transcript scraper
│   ├── services/
│   │   ├── process_anthropic.py # Fetch full article markdown
│   │   ├── process_youtube.py   # Fetch video transcripts
│   │   ├── process_digest.py    # Run digest generation
│   │   └── process_email.py     # Build and send email
│   ├── profiles/
│   │   └── user_profile.py      # Your interests and preferences
│   ├── config.py                # YouTube channel config
│   ├── daily_runner.py          # Orchestrates all 5 stages
│   └── runner.py                # Runs all scrapers
├── docker/
│   └── docker-compose.yml       # PostgreSQL container
├── main.py                      # Entry point
├── pyproject.toml               # Dependencies
└── .env                         # Your credentials (not committed)

---

## ⚙️ Setup & Installation

### Prerequisites
- Python 3.12
- PostgreSQL
- Ollama installed with LLaMA 3.2 model

### Steps

**1. Clone the repository**
```bash
git clone https://github.com/Ayushtechera/neural-news-forge.git
cd neural-news-forge
```

**2. Install dependencies**
```bash
pip install uv
uv sync
```

**3. Setup environment variables**
```bash
cp app/example.env .env
```

Fill in your `.env`:

OPENAI_API_KEY=optional
MY_EMAIL=your@gmail.com
APP_PASSWORD=your_gmail_app_password
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=ai_news_aggregator
POSTGRES_HOST=localhost
POSTGRES_PORT=5432

**4. Start PostgreSQL and create database**
```bash
psql -U postgres -c "CREATE DATABASE ai_news_aggregator;"
```

**5. Create tables**
```bash
uv run python -c "from app.database.models import Base; from app.database.connection import engine; Base.metadata.create_all(engine)"
```

**6. Pull LLaMA model via Ollama**
```bash
ollama pull llama3.2
```

**7. Run the pipeline**
```bash
uv run python main.py 24 10
```

Arguments:
- `24` → fetch articles from last 24 hours
- `10` → include top 10 articles in email

---

## 📬 Sample Email Output

The pipeline delivers a clean, formatted HTML email with:
- Personalized greeting
- AI-written introduction summarizing today's themes
- Top ranked articles with summaries and read-more links

---

## 🔄 How to Automate Daily

**Windows Task Scheduler:**
1. Open `taskschd.msc`
2. Create Basic Task → Daily
3. Action: `uv run python main.py 24 10`
4. Start in: `C:\path\to\neural-news-forge`

---

## 👨‍💻 Author

**Ayush Kashyap**
GitHub: [@Ayushtechera](https://github.com/Ayushtechera)

