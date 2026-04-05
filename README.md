# Neural News Forge 🧠

> Autonomous AI pipeline that scrapes, summarizes, ranks and delivers personalized AI news digests via email — powered by LLMs and RSS intelligence.

## What it does

Every day this pipeline automatically:
- Scrapes latest AI news from **OpenAI**, **Anthropic** RSS feeds and **YouTube** channels
- Fetches full article content and video transcripts
- Generates concise AI-powered summaries using **LLaMA 3.2**
- Ranks articles based on your personal interest profile
- Delivers a clean, formatted **email digest** to your inbox

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | Python 3.12 |
| Database | PostgreSQL |
| ORM | SQLAlchemy |
| AI Model | LLaMA 3.2 via Ollama |
| RSS Parsing | feedparser |
| Web Scraping | docling |
| Transcript | youtube-transcript-api |
| Email | smtplib + Gmail SMTP |
| Validation | Pydantic |
| Package Manager | uv |

## Project Structure