# ProScope AI – Project Document & Email Assistant

ProScope AI is an AI assistant for **project managers and consultants**.  
It ingests PDFs, Word documents, and email threads, then:

- 📚 Builds a searchable knowledge base
- 🧠 Answers questions about project context
- 📝 Summarizes long documents and meetings
- ✅ Extracts actionable tasks, owners, and deadlines
- ⚠️ Highlights risks, blockers, and dependencies

Built with **FastAPI + RAG (Retrieval-Augmented Generation) + LLMs**.

---

## ✨ Features

- Upload project documents (specifications, reports, contracts, minutes, etc.)
- Upload email-like text (copy/paste important threads)
- Ask natural language questions about the project
- Get:
  - Short & long summaries
  - Key decisions
  - Extracted tasks (who does what, by when)
  - Risks & assumptions with supporting evidence
- See which document chunks were used as sources

---

## 🧱 Tech Stack

- **Backend:** Python, FastAPI
- **AI / NLP:** Hugging Face models, RAG pipeline (embeddings + retrieval + LLM)
- **Vector DB:** Chroma / FAISS (local, simple to run)
- **DB:** SQLite (for projects, docs & history)
- **Frontend:** Streamlit (prototype UI) or simple web client
- **Packaging & Dev:** Poetry / pip + venv, Docker, GitHub

---

## 🏗️ Architecture Overview

1. **Ingestion**
   - User uploads a document or pastes an email thread.
   - Text is extracted (PDF → text, etc.), cleaned and split into chunks.

2. **Indexing**
   - Each chunk is embedded using a sentence transformer.
   - Embeddings + metadata (doc_id, project_id, page, etc.) are stored in a vector DB.

3. **Question Answering / Analysis**
   - User asks a question or selects a mode (Summary / Actions / Risks).
   - Relevant chunks are retrieved using vector similarity.
   - A prompt is built using the retrieved context.
   - An LLM generates the answer + structured JSON if needed (e.g. tasks).

4. **Frontend**
   - User sees:
     - Final answer (summary, actions, risks…)
     - Source snippets
     - Project chat history

---

## 🚀 Quickstart

```bash
# 1. Clone the repo
git clone https://github.com/your-username/proscope-ai.git
cd proscope-ai

# 2. Create and activate virtual environment (example with venv)
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run backend
uvicorn app.main:app --reload

# 5. Run Streamlit UI 
streamlit run ui/app.py
```
