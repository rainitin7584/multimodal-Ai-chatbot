# multimodal-Ai-chatbot
# 🌌 Aura: Multimodal Emotional AI Companion & Document Canvas

> **A beginner-friendly, multimodal AI companion featuring RAG (PostgreSQL + pgvector), real-time Web Search, Interactive Document Canvas, and Emotional Intelligence.**

---

## 🌟 Key Highlights & Architecture

```
                    ┌───────────────────────────────────────────┐
                    │       React (Vite) Modern Frontend        │
                    │  - Voice Input / Audio Playback (TTS)     │
                    │  - Image Upload & Vision Preview          │
                    │  - Interactive Document Canvas (Side-by)  │
                    │  - Mood / Emotional State Indicator       │
                    └─────────────────────┬─────────────────────┘
                                          │  REST / SSE / WS
                                          ▼
                    ┌───────────────────────────────────────────┐
                    │           FastAPI Backend Engine          │
                    │  ├── Multimodal Ingestion & Dispatcher    │
                    │  ├── Emotional Sentiment & Empathy Layer  │
                    │  ├── RAG Pipeline (pgvector Retriever)    │
                    │  ├── Web Search Agent (DuckDuckGo/Tavily) │
                    │  └── Document Canvas Manager (CRUD/Diff)  │
                    └─────────────────────┬─────────────────────┘
                                          │
                  ┌───────────────────────┴───────────────────────┐
                  ▼                                               ▼
      ┌─────────────────────────┐                     ┌─────────────────────────┐
      │   Multimodal AI APIs    │                     │  PostgreSQL + pgvector  │
      │  (Gemini / OpenAI)      │                     │  - Chat Sessions & Logs │
      │  - Vision, Speech, Text │                     │  - Document Embeddings  │
      │  - Image Gen & Search   │                     │  - Canvas Documents     │
      └─────────────────────────┘                     └─────────────────────────┘
```

---

## 🚀 Core Functionalities

| Feature | Capability | Implementation Detail |
| :--- | :--- | :--- |
| 🎙️ **Multimodal Inputs** | Text, Audio/Voice recordings, Images, PDFs/TXTs | Web Audio API + Whisper/Gemini Audio, Vision models |
| 🎨 **Multimodal Outputs** | Markdown, Speech (TTS), Generated Images, Cards | Web Speech / TTS API, Image generation, rich React cards |
| 🌐 **Live Web Search** | Real-time information answering with citations | DuckDuckGo Search / Tavily API agentic tool calling |
| 📚 **RAG Architecture** | Semantic search across attached documents | `pgvector` extension in PostgreSQL, cosine similarity |
| 📝 **Document Canvas** | Create, view, iteratively update & export documents | Split-view canvas, versioned document updates |
| 💖 **Emotional Companion** | Empathetic listening, warm tone, sentiment aware | Sentiment prompt-steering, warm supportive persona |
| ⚡ **Zero Auth / Frictionless**| Instant session-based chatting without signups | Client-persisted session keys, no login barrier |

---

## 🛠️ Tech Stack

- **Frontend**: [React 18+](https://react.dev/) + [Vite](https://vitejs.dev/) + Modern Vanilla CSS / CSS Modules + Lucide Icons
- **Backend**: [Python 3.10+](https://www.python.org/) + [FastAPI](https://fastapi.tiangolo.com/) + Uvicorn + Pydantic v2
- **Vector Database**: [PostgreSQL](https://www.postgresql.org/) with [`pgvector`](https://github.com/pgvector/pgvector)
- **AI & Embedding Models**: Google Gemini 1.5/2.0 API (or OpenAI GPT-4o / Whisper / Embeddings)
- **Search Tooling**: `duckduckgo-search` or `tavily-python`

---

## 📂 Project Structure

```
MM chatbot/
├── backend/
│   ├── app/
│   │   ├── api/
│   │   │   ├── chat.py           # Chat completions & SSE streaming
│   │   │   ├── documents.py      # Canvas document CRUD & updates
│   │   │   ├── rag.py            # Document upload & vector ingestion
│   │   │   └── search.py         # Web search router
│   │   ├── core/
│   │   │   ├── config.py         # Environment & settings
│   │   │   └── database.py       # Async SQLAlchemy / asyncpg setup
│   │   ├── models/
│   │   │   ├── db_models.py      # SQLAlchemy ORM (Messages, Canvas, Embeddings)
│   │   │   └── schemas.py        # Pydantic request/response schemas
│   │   ├── services/
│   │   │   ├── ai_service.py     # Multimodal LLM orchestration
│   │   │   ├── emotional_core.py # Sentiment analysis & emotional prompt crafting
│   │   │   ├── rag_service.py    # Chunking, embeddings & vector retrieval
│   │   │   └── search_service.py # Web search integration
│   │   └── main.py               # FastAPI entry point
│   ├── requirements.txt
│   ├── .env.example
│   └── Dockerfile
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Chat/             # Message list, bubble, input bar, voice recorder
│   │   │   ├── Canvas/           # Interactive document canvas (preview & edit)
│   │   │   ├── Emotional/        # Mood badge & empathy pulse indicators
│   │   │   └── Media/            # Audio player & image attachment preview
│   │   ├── hooks/
│   │   │   ├── useChat.js        # Chat state & SSE streaming hook
│   │   │   └── useAudioRecorder.js# Mic recording utility
│   │   ├── styles/
│   │   │   └── index.css         # Modern glassmorphic theme
│   │   ├── App.jsx               # Layout split (Chat + Canvas)
│   │   └── main.jsx
│   ├── package.json
│   └── vite.config.js
│
├── docker-compose.yml            # PostgreSQL with pgvector + Backend + Frontend
└── README.md
```

---

## ⚡ Quickstart Guide

### 1. Prerequisites
- **Python 3.10+**
- **Node.js 18+ & npm**
- **PostgreSQL with `pgvector`** (or run via Docker)
- API key for Gemini (`GEMINI_API_KEY`) or OpenAI (`OPENAI_API_KEY`)

---

### 2. Database Setup (Fastest with Docker)

Run a PostgreSQL instance preconfigured with `pgvector`:

```bash
docker run -d \
  --name mm-postgres \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=postgres \
  -e POSTGRES_DB=mmchatbot \
  -p 5432:5432 \
  pgvector/pgvector:pg16
```

---

### 3. Backend Setup

```bash
# Navigate to backend
cd backend

# Create virtual environment
python -m venv venv
# On Windows:
venv\Scripts\activate
# On Mac/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Create .env file
cp .env.example .env
```

**Sample `.env`:**
```ini
DATABASE_URL=postgresql+asyncpg://postgres:postgres@localhost:5432/mmchatbot
GEMINI_API_KEY=your_gemini_api_key_here
TAVILY_API_KEY=your_tavily_key_or_leave_blank_for_duckduckgo
PORT=8000
```

**Run Backend:**
```bash
uvicorn app.main:app --reload --port 8000
```
API Documentation will be available at: `http://localhost:8000/docs`

---

### 4. Frontend Setup

```bash
# Navigate to frontend
cd ../frontend

# Install dependencies
npm install

# Start development server
npm run dev
```
Open `http://localhost:5173` in your browser.

---

## 💡 Usage Walkthrough

1. **Multimodal Conversation**:
   - Tap the **Mic** icon to speak your thoughts.
   - Attach an **Image** to ask questions about it or seek creative advice.
2. **Emotional Support**:
   - Share personal stress or daily events; the companion dynamically tunes its warmth, offers active listening, and suggests reflective grounding exercises.
3. **Document Canvas**:
   - Say: *"Draft a calm morning routine guide for me"* -> The Document Canvas automatically slides in from the right with formatted markdown.
   - Say: *"Add a 5-minute meditation step to the morning routine"* -> The assistant updates the live document canvas while tracking version history.
4. **Live Web Search**:
   - Ask about today's events, recent scientific studies, or weather updates; the bot executes live search queries and cites sources cleanly.
5. **Knowledge RAG**:
   - Drag & drop personal notes, manuals, or study guides. The bot indexes them into `pgvector` and accurately answers questions with page/chunk references.

---

## 🔒 Roadmap & Future Enhancements

- [ ] Optional multi-user accounts & persistent cloud sync
- [ ] Voice-to-voice bidirectional streaming (WebRTC)
- [ ] Advanced canvas export (Export to PDF, Notion, Google Docs)
- [ ] Long-term emotional memory graph with user consent

---

## 📄 License
MIT License. Built with ❤️ for multimodal AI exploration.
