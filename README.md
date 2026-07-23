# 🎓 Study Assistant RAG

> Ask your course documents exam-style questions and get 
> accurate answers — no hallucinations, no outside knowledge.

## What It Does

Upload any lecture note or course PDF, then ask it questions 
the way a lecturer would in an exam. The assistant answers 
**only from your material** — nothing else.

## How It Works

**Step 1 — Load your document (once)**

Manual Trigger → HTTP Request (Google Drive PDF)
→ Document Loader → Qdrant Vector Store
↑
Embeddings Google Gemini

**Step 2 — Ask questions (every time)**

Chat Trigger → Qdrant Vector Store (semantic search)
↑
Embeddings Google Gemini
↓
Code Node
(builds context)
↓
Basic LLM Chain → Groq
↓
Respond to Webhook

## Tech Stack

| Tool | Role |
|------|------|
| [n8n](https://n8n.io) | Workflow automation — no code |
| [Google Gemini](https://aistudio.google.com) | Embeddings (`text-embedding-004`) |
| [Qdrant](https://qdrant.tech) | Vector database |
| [Groq](https://console.groq.com) | LLM — fast free inference |
| [Railway](https://railway.app) | Hosts n8n 24/7 |

## Key Design Decisions

- **Gemini for embeddings only** — most accurate at 768 dimensions
- **Groq as LLM** — faster and free tier friendly
- **Qdrant over Pinecone** — better free tier, clean REST API
- **Webhook + CORS** — accessible from any interface
- **Simple Memory** — maintains conversation context per session
- **Manual linear pipeline** — explicit control over retrieval 
  and context injection, no black-box agent

## Project Structure

study-assistant-rag/
├── README.md
├── .gitignore
└── workflows/
├── ingestion.json ← loads PDF into Qdrant
└── chat.json ← answers questions via chat

## Build Stages
- [x] Stage 1: Accounts & GitHub setup
- [x] Stage 2: n8n hosted on Railway
- [x] Stage 3: Document ingestion pipeline
- [x] Stage 4: Query & answer pipeline
- [x] Stage 5: Telegram bot connected
- [x] Stage 6: Final documentation

## Author
**Promise O. Amhanesi** — Founder, AMHANi Enterprise  
Building AI-powered tools for finance and education.
