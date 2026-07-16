# Course Companion — AI-powered learning platform

A learning platform with an AI assistant that actually knows the course. Students browse curriculum content, chat with a RAG-grounded AI tutor, review their personal conversation history, and discuss in a community forum where every new post gets an automated, context-aware AI reply.

Built as my capstone for Le Wagon's AI Product Builder course. I owned the full arc: problem framing, KPI definition, POC architecture, build, and documentation.

🎬 [Demo](https://youtu.be/9r1g6I0wlGs) · [Full technical walkthrough (7 min)](https://youtu.be/tosVH4YtQhU)

<img width="1470" height="956" alt="Screenshot 2026-05-30 at 14 30 11" src="https://github.com/user-attachments/assets/f336bfbc-25ee-43b2-bdd2-4f8311b381e0" />
<img width="1470" height="956" alt="Screenshot 2026-05-30 at 14 31 45" src="https://github.com/user-attachments/assets/8211ad62-056a-4fca-9d8f-8ca410cb2c47" />
<img width="1251" height="975" alt="Screenshot 2026-07-16 at 15 48 53" src="https://github.com/user-attachments/assets/403bc51a-235a-4c83-aa63-bace616121bf" />
<img width="1462" height="851" alt="Screenshot 2026-07-16 at 15 50 04" src="https://github.com/user-attachments/assets/0bea1137-43c1-497a-bbfe-b2147806bfd5" />


<table>
  <tr>
    <td width="50%">
      <a href="https://github.com/user-attachments/assets/f336bfbc-25ee-43b2-bdd2-4f8311b381e0">
        <img src="https://github.com/user-attachments/assets/f336bfbc-25ee-43b2-bdd2-4f8311b381e0" alt="Journal entry view" width="100%">
      </a>
    </td>
    <td width="50%">
      <a href="https://github.com/user-attachments/assets/8211ad62-056a-4fca-9d8f-8ca410cb2c47">
        <img src="https://github.com/user-attachments/assets/8211ad62-056a-4fca-9d8f-8ca410cb2c47" alt="Entry list" width="100%">
      </a>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <a href="https://github.com/user-attachments/assets/403bc51a-235a-4c83-aa63-bace616121bf">
        <img src="https://github.com/user-attachments/assets/403bc51a-235a-4c83-aa63-bace616121bf" alt="Bot conversation" width="100%">
      </a>
    </td>
    <td width="50%">
      <a href="https://github.com/user-attachments/assets/0bea1137-43c1-497a-bbfe-b2147806bfd5" >
        <img src="https://github.com/user-attachments/assets/0bea1137-43c1-497a-bbfe-b2147806bfd5" alt="Settings panel" width="100%">
      </a>
    </td>
  </tr>
</table>

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
