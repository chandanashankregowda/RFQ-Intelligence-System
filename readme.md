# 🧠 Agentic AI RFQ Intelligence Platform (Production RAG System)

## 📌 Data Source
Google Drive:
https://drive.google.com/drive/folders/1vBMW7ACTXMqwJpngg66SjzG0skxvt5Ww?usp=drive_link

---

# 🚀 0. PROJECT OBJECTIVE

## 🎯 Goal

Build a **production-grade Agentic AI system** that:

- Ingests RFQ PDFs from Google Drive
- Fetches live procurement bids from API
- Builds a RAG system over historical RFQs
- Uses AI agents to reason across:
  - historical RFQs
  - live bids
  - product specs
  - compliance rules
- Generates structured procurement recommendations

---

## 🧠 Real-World Use Case

Procurement teams today manually:

- Read RFQ PDFs
- Search past projects
- Compare requirements manually
- Identify suitable products

👉 This system automates all of that using AI agents + RAG.

---

## 🏁 FINAL OUTPUT EXAMPLE

3 relevant bids found:

1. Judicial Branch LED Retrofit (Closing in 5 days)
2. California School Lighting Upgrade
3. City Hospital Lighting Expansion

Similar Past RFQs:
- Hospital LED Retrofit 2025

Recommendation:
- Use UL 1598 certified LED panels
- Prefer 4000K neutral white lighting
- Use corrosion-resistant outdoor fixtures

---

# 🏗️ 1. SYSTEM ARCHITECTURE

## Components

### 1. Data Layer
- Google Drive (RFQs, manuals, catalogs)
- Procurement API (live bids)

### 2. Processing Layer
- PDF extraction
- cleaning
- chunking

### 3. RAG Layer
- embeddings
- vector database (Chroma / FAISS)

### 4. Agent Layer
- tool calling system
- multi-step reasoning

### 5. Backend Layer
- FastAPI service

### 6. Monitoring Layer
- logs + evaluation metrics

---

# ⚙️ 2. TECH STACK

- Python 3.10+
- FastAPI
- LangChain / LangGraph
- ChromaDB or FAISS
- PyMuPDF
- OpenAI / embeddings model
- Docker

---

# 📦 3. IMPLEMENTATION PHASES

---

# 🟦 PHASE 1 — PROJECT SETUP

## Tasks

- Create project structure:

rfq-system/
├── app/
│   ├── ingestion/
│   ├── rag/
│   ├── agents/
│   ├── tools/
│   ├── api/
├── data/
├── vector_db/
├── main.py

- Install dependencies:

pip install fastapi langchain chromadb pymupdf pandas requests

---

# 🟩 PHASE 2 — GOOGLE DRIVE INGESTION

## Tasks

- Setup Google Cloud project
- Enable Drive API
- Create service account
- Authenticate and access RFQ folder
- Download PDFs automatically

## Output

File metadata structure:

- file_name
- file_id
- last_modified

---

# 🟨 PHASE 3 — PDF PROCESSING

## Tasks

- Extract text using PyMuPDF
- Convert PDF → structured text
- Maintain page-level metadata

## Cleaning rules

Remove:
- headers
- footers
- page numbers

---

# 🟧 PHASE 4 — CHUNKING

## Rules

- Chunk size: 800–1200 tokens
- Overlap: 150–200 tokens
- Preserve metadata

## Output

Each chunk contains:

- text
- doc_id
- page number

---

# 🟪 PHASE 5 — EMBEDDINGS

## Tasks

- Convert chunks into embeddings
- Use OpenAI or sentence-transformers
- Store vectors

---

# 🟥 PHASE 6 — VECTOR DATABASE

## Tasks

- Store embeddings in ChromaDB / FAISS
- Enable semantic search

## Flow

User Query → Embedding → Vector Search → Top-K chunks

---

# 🟫 PHASE 7 — PROCUREMENT API

API:
https://bid-data.onrender.com/bid

## Tasks

- Fetch live bids
- Normalize JSON
- Convert to structured dataset
- Schedule periodic updates

---

# 🟦 PHASE 8 — RAG RETRIEVAL ENGINE

## Flow

User Query →
Embedding →
Vector DB Search →
Top-K RFQ chunks

---

# 🟩 PHASE 9 — CONTEXT FUSION

Combine:

- RFQ historical data (RAG)
- Live bids (API)

Final merged context is sent to LLM.

---

# 🧠 PHASE 10 — AGENT SYSTEM

## Tools

- Drive Tool → fetch RFQs
- API Tool → fetch bids
- Web Tool → compliance checks

## Behavior

Agent decides:

- when to search documents
- when to call API
- when to use web search

---

# 🧾 PHASE 11 — RESPONSE GENERATION

## Output format

- Bid summary
- Matching RFQs
- Recommendations
- Compliance notes

---

# 🚀 PHASE 12 — DEPLOYMENT

## Backend

FastAPI endpoints:

- /query → main agent interface
- /ingest → trigger ingestion
- /bids → fetch live bids

## Deployment

- Docker container
- Deploy on AWS / GCP / Azure

---

# 📊 PHASE 13 — MONITORING

Track:

- retrieval accuracy
- response latency
- hallucination rate
- bid match quality

Use:

- logging system
- LangSmith (optional)

---

# 🏁 FINAL SYSTEM BEHAVIOR

System acts as:

👉 Autonomous AI Procurement Analyst

It can:

- read RFQs
- monitor live bids
- retrieve past knowledge
- generate recommendations
- assist in real bidding decisions
