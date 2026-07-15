# Course Companion — AI-powered learning platform

A learning platform with an AI assistant that actually knows the course. Students browse curriculum content, chat with a RAG-grounded AI tutor, review their personal conversation history, and discuss in a community forum where every new post gets an automated, context-aware AI reply.

Built as my capstone for Le Wagon's AI Product Builder course. I owned the full arc: problem framing, KPI definition, POC architecture, build, and documentation.

🎬 [Demo](https://youtu.be/9r1g6I0wlGs) · [Full technical walkthrough (7 min)](https://youtu.be/tosVH4YtQhU)

Screenshot: course explorer -->
Screenshot: RAG chatbot answering a course question -->
Screenshot: n8n orchestration workflows -->

## Architecture

**Frontend** — Softr handles the UI, authentication, dynamic content blocks, and visibility rules (users only see their own data).

**Database** — Airtable stores the relational schema: users, course chapters, conversations, messages, forum posts, and comments, connected via linked records.

**RAG pipeline** — course content is chunked, embedded, and stored as vectors in Supabase (pgvector). At query time, n8n retrieves the most relevant chunks and grounds the GPT response in real course material rather than generic knowledge.

**Orchestration** — n8n runs everything behind the scenes: the chat workflow, conversation tracking, AI title generation, and a forum auto-responder that triggers on every new post and answers from the same knowledge base.

**User attribution** — the logged-in user's identity is passed as metadata from Softr to n8n with every message and persisted in Airtable, enabling a secure, personal conversation history.

## Tech stack

- **Softr** — frontend, auth, access control
- **Airtable** — relational database (6 linked tables)
- **Supabase** — PostgreSQL vector store (pgvector) for RAG retrieval
- **n8n** — workflow automation and AI orchestration
- **OpenAI** — GPT for chat, titles, and forum replies; embedding model for vectorisation

## Repo contents

- `workflows/` — exported n8n workflows (RAG chatbot, ingestion pipeline, forum auto-responder; credentials stripped)
- `docs/` — Airtable schema overview and screenshots

## Key learnings

- **RAG from scratch** — chunking, embedding, similarity search, and context-grounded responses as one coherent pipeline
- **Relational schema design** — structuring a multi-table Airtable base that behaves like a real application backend
- **Secure user attribution** — passing authenticated identity from frontend to backend via metadata and persisting the link on every interaction
- **Event-driven vs. scheduled automation** — trade-offs between instant webhooks and free-tier polling triggers
- **No-code/low-code product development** — composing Softr, Airtable, n8n, and Supabase into one product without traditional application code
