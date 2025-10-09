# Knowledge-Based Search Engine

Monorepo containing a document-grounded chat experience built with a FastAPI backend and a Next.js frontend. Authenticated users can upload PDFs, curate the context shared with the model, and converse with an AI assistant that retrieves relevant snippets from their personal knowledge base.

## Repository Layout

```
.
├── backend/    # FastAPI service, Supabase integration, embeddings + vector search
├── frontend/   # Next.js App Router client, Supabase auth, chat UI
├── .gitignore
└── README.md   # You are here
```

Each subdirectory contains its own README describing local setup.

## Quick Start

> **Prerequisites**
> - Python 3.10+
> - Node.js 18+ (or newer that is supported by Next.js 15)
> - Supabase project with storage bucket and service/config keys
> - Google Generative AI API key (Gemini)

1. **Clone & install**
   ```bash
   git clone <repo-url>
   cd knowledge-based-search-engine
   ```

2. **Backend**
   ```bash
   cd backend
   python -m venv .venv && source .venv/bin/activate
   pip install -r requirements.txt
   cp .env.example .env  # create one if it doesn't exist
   ```
   Update environment variables in `.env` (see `backend/README.md` for details) then run:
   ```bash
   uvicorn backend.main:app --reload
   ```

3. **Frontend**
   ```bash
   cd ../frontend
   npm install
   cp .env.local.example .env.local  # create one if missing
   npm run dev
   ```
   Browse to <http://localhost:3000>.

The frontend automatically injects Supabase auth tokens and the current `user_id` into every API call. The backend enforces that the authenticated Supabase user matches the requested resources while retrieving embeddings and generating LLM responses using Gemini.

## Key Features

- Supabase-authenticated conversations scoped per user
- PDF ingestion to Supabase Storage with FAISS-powered retrieval
- Gemini model responses constrained to retrieved context
- Rich chat interface with mobile drawers, inline document preview, drag-free layout
- Conversation renaming and bulk deletion (documents, messages, vectors) handled server-side

## Development Notes

- See `frontend/README.md` and `backend/README.md` for environment variables, scripts, and troubleshooting.
- The repo currently ships without linting/format hooks; configure ESLint/Prettier or Ruff/Black as needed.
- Secrets checked into the sample `.env` files are placeholders—replace them with your own credentials before deploying.

## License

MIT — use freely with attribution.
