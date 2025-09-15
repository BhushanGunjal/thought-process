# Technologies

* **Streamlit** (UI)
* **FastAPI** (backend API)
* **LangGraph** (agents/orchestrator)
* **ChromaDB** (vector DB)
* **OpenAI API**

---

#  Project Folder Structure

```
chatbot/
│
├── UI/                          # Streamlit frontend
│   ├── app.py                   # Main Streamlit app (chat interface, file upload)
│   └── components/              # (Optional) custom UI widgets
│
├── API/                         # FastAPI backend
│   ├── main.py                  # FastAPI entry point
│   ├── routes/                  # API endpoints
│   │   ├── chat.py              # POST /chat endpoint
│   │   ├── upload.py            # POST /upload endpoint
│   │   └── history.py           # GET /history endpoint
│   ├── models/                  # Pydantic models (request/response schemas)
│   │   ├── chat_models.py
│   │   └── upload_models.py
│   └── utils/                   # Helper functions (JWT, logging, etc.)
│
├── UPLOAD/                      # File ingestion & preprocessing
│   ├── processor.py             # Extract text from PDFs/Docs
│   ├── embeddings.py            # Generate embeddings via OpenAI
│   └── storage/                 # Saved user-uploaded files
│
├── AGENTS/                      # LangGraph agents + orchestration
│   ├── orchestrator.py          # LangGraph Orchestrator (entry point)
│   ├── graph.py                 # Define nodes + edges (planner, retrieval, etc.)
│   ├── planner.py               # Planner Agent (routing logic)
│   ├── retrieval.py             # Retrieval Agent (ChromaDB search)
│   ├── summarizer.py            # Summarizer Agent
│   ├── reasoning.py             # Reasoning Agent
│   └── tools/                   # (Optional) math tools, web search, etc.
│
├── DB/                          # Databases
│   ├── chroma/                  # ChromaDB persistent storage
│   └── sqlite/                  # (Optional) SQLite for chat history, users
│
├── config/                      # Configuration & secrets
│   ├── settings.py              # API keys, DB paths, env variables
│   └── logging.yaml             # Logging config
│
├── tests/                       # Unit & integration tests
│   ├── test_api.py
│   ├── test_agents.py
│   └── test_upload.py
│
├── docker-compose.yml           # (Optional) Run all services easily
├── requirements.txt             # Python dependencies
├── README.md                    # Documentation
└── .env                         # Environment variables (API keys, etc.)
```

---

#  Flow Between Folders

* **UI** → sends queries/files → **API**
* **API** → calls → **AGENTS/orchestrator.py**
* **AGENTS** → uses **UPLOAD** (for embeddings) + **DB** (ChromaDB)
* **Orchestrator** → runs LangGraph workflow → sends back response

---

 This structure is modular:

* Can swap **ChromaDB** with **Pinecone/Weaviate** later (just update `retrieval.py`).
* Can add new agents (math, translation, etc.) in `AGENTS/tools/`.
* Streamlit can be replaced with React frontend later, API remains unchanged.

---

