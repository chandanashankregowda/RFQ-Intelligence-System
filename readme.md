# Smart RFQ / Bid Response Agent (Agentic AI + RAG System)

---

# 1. Problem Statement

## Business Context

Organizations receive RFQs containing:

- Large PDF documents (50–300 pages)
- Technical specifications
- Bills of Quantity (BOQ)
- Compliance standards (UL, ISO, IEC)
- Installation and environmental constraints

---

## Current Manual Workflow

- Reading RFQ documents manually (2–6 hours)
- Extracting requirements manually
- Searching past projects manually
- Matching products manually
- Preparing bid responses manually

---

## Key Problems

- Slow processing time
- High dependency on domain experts
- Human errors in compliance interpretation
- Inconsistent bid quality
- Lost business opportunities

---

# 2. System Objective

## Goal

Build an autonomous RFQ intelligence system that:

- Ingests RFQ PDFs automatically
- Extracts structured requirements
- Retrieves similar past RFQs using RAG
- Fetches live bid data from API
- Generates structured procurement responses

---

## Expected Output

System must generate:

- RFQ summaries
- Product recommendations
- Compliance checks
- Similar past RFQs
- Missing requirement analysis

---

# 3. Performance Requirements

## Response Time Targets

- Simple query: 2–4 seconds
- Medium RFQ: 5–10 seconds
- Large RFQ: 10–20 seconds
- Full reasoning pipeline: under 25 seconds

---

## Requirement Rationale

The system must support procurement workflows where:

- Multiple bids are evaluated quickly
- Decisions are time-sensitive
- Latency directly impacts business outcomes

---

# 4. System Architecture

## Core Layers

### Input Layer
- RFQ PDFs from Google Drive
- Chat or API queries

### Processing Layer
- PDF extraction
- Text cleaning
- Structure detection

### RAG Layer
- Embedding generation
- Vector database (FAISS or Chroma)
- Semantic retrieval

### Agent Layer
- Tool selection
- Multi-step reasoning
- Decision orchestration

### Backend Layer
- FastAPI service
- Async execution

### Monitoring Layer
- Logs
- Latency tracking
- Evaluation metrics

---

# 5. Technology Stack

- Python 3.10+
- FastAPI
- LangChain or LangGraph
- FAISS or ChromaDB
- PyMuPDF
- OpenAI embeddings or sentence-transformers
- Docker

---

# 6. Implementation Phases

---

# Phase 1: Project Setup

## Objective

Establish production-grade project structure

## Structure

rfq-system/
- app/
  - ingestion/
  - processing/
  - rag/
  - agents/
  - tools/
  - api/
- data/
- vector_db/
- logs/
- main.py
- requirements.txt

## Dependencies

pip install fastapi langchain langgraph chromadb pymupdf pandas requests python-dotenv

---

# Phase 2: Google Drive Ingestion

## Objective

Automate RFQ PDF ingestion from Google Drive

https://drive.google.com/drive/folders/1vBMW7ACTXMqwJpngg66SjzG0skxvt5Ww?usp=drive_link

## Steps

- Create Google Cloud project
- Enable Google Drive API
- Create service account
- Authenticate application
- Access RFQ folder

## System Behavior

- Detect new files
- Download PDFs automatically
- Track file changes

## Output

{
  "file_name": "hospital_rfq.pdf",
  "file_id": "abc123",
  "last_modified": "2026-05-01"
}

---

# Phase 3: PDF Processing

## Objective

Convert RFQ PDFs into structured text

## Steps

- Extract text using PyMuPDF
- Preserve page structure
- Remove headers, footers, and noise

## Output

{
  "doc_id": "RFQ_001",
  "page": 3,
  "text": "All LED fixtures must comply with UL 1598 standards."
}

---

# Phase 4: Chunking

## Objective

Prepare documents for embedding and retrieval

## Rules

- Chunk size: 800–1200 tokens
- Overlap: 150–200 tokens
- Maintain semantic boundaries

## Output

{
  "chunk_id": "c001",
  "text": "Outdoor lighting must withstand corrosion...",
  "doc_id": "RFQ_001",
  "page": 4
}

---

# Phase 5: Embedding Generation

## Objective

Convert text chunks into vector representations

## Steps

- Generate embeddings using OpenAI or sentence-transformers
- Store embeddings with metadata

---

# Phase 6: Vector Database

## Objective

Enable semantic search over RFQ knowledge

## Flow

User Query → Embedding → Vector Search → Top-K Results

---

# Phase 7: Procurement API Integration

## API Endpoint

https://bid-data.onrender.com/bid

## Steps

- Fetch live bid data
- Normalize JSON response
- Filter by:
  - deadline
  - department
  - status

## Output

{
  "event_name": "LED Retrofit Project",
  "department": "Government Housing",
  "deadline": "2026-05-15"
}

---

# Phase 8: RAG Retrieval Engine

## Flow

User Query → Embedding → Vector Database → Top-K RFQ chunks

---

# Phase 9: Context Fusion

## Objective

Merge multiple data sources into a single context

## Inputs

- Historical RFQ data from vector database
- Live bid data from API

## Output

{
  "rfq_context": [],
  "live_bids": [],
  "final_context": "merged input"
}

---

# Phase 10: Agent System

## Tools

- Drive Tool: RFQ retrieval
- API Tool: live bid fetching
- Web Tool: compliance and standards lookup

## Behavior

Agent decides:

- when to retrieve documents
- when to call APIs
- when to use web search
- how to merge information

---

# Phase 11: Response Generation

## Output Format

- RFQ Summary
- Requirements extraction
- Similar past RFQs
- Product recommendations
- Missing information

---

# Phase 12: Deployment

## Backend

FastAPI endpoints:

- POST /query
- POST /ingest
- GET /bids

## Infrastructure

- Docker containerization
- Cloud deployment (AWS, GCP, or Azure)

## Background Jobs

- Drive sync every hour
- API sync every 30 minutes

---

# Phase 13: Monitoring

## Metrics

- Retrieval accuracy
- Response latency
- Hallucination rate
- Bid matching quality

## Tools

- Structured logging
- LangSmith (optional)
- OpenTelemetry (optional)

---

# Final System Behavior

The system behaves as an autonomous procurement intelligence assistant that:

- Reads RFQs automatically
- Extracts structured requirements
- Matches historical knowledge
- Analyzes live bids
- Generates structured responses within seconds

---

# Final Outcome

A production-grade Agentic AI + RAG system for RFQ intelligence automation in real-world procurement workflows.
