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

---

# RFQ / RFP Agent Evaluation Set (Lighting Retrofit Documents)

---

# 1. Document Understanding Tasks

## Q1
Input:
"Summarize the League City Retrofit Lighting RFP"

Expected Output:
- Project type: municipal lighting retrofit
- Scope: replace existing lighting with energy-efficient LED systems
- Sites included: public buildings / streets / facilities (as per document)
- Key goals: energy savings, compliance, maintenance reduction
- Bid requirement overview: submission format, deadlines, compliance docs

---

## Q2
Input:
"What is the scope of work in the City of Scranton LED Retrofit Bid?"

Expected Output:
- LED replacement across municipal infrastructure
- Removal of existing lighting fixtures
- Installation of energy-efficient LED systems
- Testing and commissioning requirements
- Disposal of old fixtures (if mentioned)
- Maintenance / warranty obligations

---

## Q3
Input:
"Extract key technical requirements from California Judicial Council Lighting RFP"

Expected Output:
- Lighting efficiency standards
- Compliance requirements (energy codes / UL / Title 24 if applicable)
- Fixture specifications (LED type, wattage range)
- Control systems (dimming / automation if included)
- Safety and installation standards

---

# 2. Compliance & Constraints

## Q4
Input:
"What compliance standards are required in these government lighting RFPs?"

Expected Output:
- Energy efficiency standards (state/federal codes)
- UL certification requirements
- Electrical safety standards
- Environmental compliance (energy conservation mandates)
- Local government procurement rules

---

## Q5
Input:
"Are there any strict installation constraints in school district lighting projects?"

Expected Output:
- Work must be done during non-school hours (if specified)
- Safety compliance for students/staff
- Noise and disruption restrictions
- Phased installation requirements
- Restricted access zones

---

# 3. Product Recommendation Tasks

## Q6
Input:
"What LED products are suitable for Irvine Unified School District Lighting Retrofit?"

Expected Output:
- LED panel lights (4000K–5000K range)
- High-efficiency ceiling fixtures
- Motion sensor-enabled lighting systems
- Low glare educational environment lighting
- Long-life (>50,000 hours) fixtures

---

## Q7
Input:
"Suggest lighting solutions for government retrofit projects"

Expected Output:
- High-efficiency LED retrofit kits
- Smart lighting controls (dimming + occupancy sensors)
- Outdoor-rated LED fixtures (IP65+)
- Energy Star certified products
- Modular retrofit systems for scalability

---

## Q8
Input:
"What is the most cost-effective solution for large-scale municipal lighting retrofit?"

Expected Output:
- Bulk LED retrofit kits
- Standardized fixture replacement strategy
- Reduced wiring modification approach
- Use of existing fixture housings where possible
- Phased deployment strategy

---

# 4. Bid Intelligence & Matching

## Q9
Input:
"Which of these RFPs are similar in structure?"

Expected Output:
- League City Retrofit ↔ City of Scranton (municipal retrofit similarity)
- California Judicial Council ↔ Irvine School District (institutional lighting upgrade)
- Similarity reasoning based on:
  - scope (retrofit)
  - sector (government/education)
  - compliance type

---

## Q10
Input:
"Match past RFQs with current lighting retrofit projects"

Expected Output:
- Hospital lighting retrofit ↔ government facility retrofit
- School lighting upgrade ↔ Irvine school district RFP
- Municipal street lighting ↔ League City project
- Similarity scoring (high/medium/low)

---

## Q11
Input:
"Which RFP has the highest technical complexity?"

Expected Output:
- California Judicial Council Lighting RFP
Reason:
- strict compliance requirements
- multi-site complexity
- advanced energy regulations
- legal/government oversight

---

# 5. Bid Strategy & Decision Making

## Q12
Input:
"Should we bid on the League City Retrofit Lighting project?"

Expected Output:
- Bid recommendation (Yes/No/Maybe)
- Reasoning:
  - scope alignment
  - competition level (if inferred)
  - compliance readiness
  - product match availability
- Risk factors
- Opportunity score (0–100)

---

## Q13
Input:
"What is the winning strategy for school district lighting projects?"

Expected Output:
- low-disruption installation strategy
- energy efficiency positioning
- safety compliance emphasis
- long-term maintenance advantage
- cost optimization approach

---

# 6. Document Intelligence

## Q14
Input:
"What are the key deadlines and submission rules?"

Expected Output:
- bid submission deadline(s)
- document format requirements
- mandatory certifications
- pre-bid meeting requirements
- evaluation criteria summary

---

## Q15
Input:
"What information is missing or unclear in these RFPs?"

Expected Output:
- incomplete electrical load details (if any)
- missing fixture counts (if not specified)
- unclear installation schedule
- missing pricing breakdown structure
- missing site measurement details

---

# 7. Multi-Document Reasoning

## Q16
Input:
"Compare municipal vs school district lighting RFPs"

Expected Output:
- Municipal:
  - outdoor + infrastructure focus
  - higher durability requirements
- School District:
  - indoor lighting focus
  - strict safety + low disruption
- Differences in compliance, installation timing, and product types

---

## Q17
Input:
"Which RFP is easiest to execute?"

Expected Output:
Ranking:
1. Municipal simple retrofit (low complexity)
2. School district lighting upgrade (medium complexity)
3. Judicial council lighting (high complexity)

Reasoning:
- compliance strictness
- site complexity
- installation constraints

---

# 8. System Explainability

## Q18
Input:
"Explain how this recommendation was generated"

Expected Output:
- Retrieved RFQs from vector DB
- Matched lighting retrofit patterns
- Extracted compliance constraints
- Filtered product catalog
- Generated final reasoning via LLM

---

## Q19
Input:
"What sources were used?"

Expected Output:
- League City Retrofit RFP
- City of Scranton LED Bid Docs
- California Judicial Council Lighting RFP
- Irvine Unified School District RFP
- Chunk references from vector database

---

# 9. Advanced Agentic Task

## Q20
Input:
"Find all active lighting retrofit opportunities, match them with past RFQs, and recommend best bidding strategy"

Expected Output:
- List of active bids (API)
- Matched historical RFQs (RAG)
- Similarity mapping
- Ranked opportunities
- Final bidding strategy:
  - which to prioritize
  - risk vs reward
  - product alignment
