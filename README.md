# cf_ai_tacoma_agent

An AI-powered chat application built on **Cloudflare Workers, D1, and Pages** that allows users to ask natural-language questions about a Toyota Tacoma owner’s manual.  
The system performs document ingestion, keyword-based retrieval, and (optionally) LLM-based answer generation using Cloudflare Workers AI.

This project demonstrates how to build a lightweight Retrieval-Augmented Generation (RAG) style application entirely on Cloudflare’s edge platform.

---

## Live Demo

**Chat UI (Cloudflare Pages):**  
https://cf-ai-tacoma-agent.pages.dev

**API Worker:**  
https://super-wood-6e6a.ritvik2.workers.dev

---

## What This Project Does

1. **Document Ingestion**
   - Manual text is chunked and stored in **Cloudflare D1**
   - Each chunk is associated with a `docId`, page range, and chunk index

2. **User Question Flow**
   - User submits a question via a chat UI
   - The Worker:
     - Extracts keywords from the question
     - Queries D1 using `LIKE` search
     - Returns the most relevant manual excerpts
     - (Optionally) sends those excerpts to an LLM for answer generation

3. **Chat UI**
   - Simple single-page UI hosted on **Cloudflare Pages**
   - Permanently connected to a specific Worker and document (`tacoma-manual`)
   - Displays answers along with citations for transparency

---

## Architecture Overview


---

## Cloudflare Services Used

- **Workers** – API routing, retrieval logic, and orchestration
- **D1** – Storage for document chunks and metadata
- **Pages** – Static frontend hosting
- **Workers AI** – Optional LLM-based answer generation

---

## Repository Structure

cf_ai_tacoma_agent/
├── worker.js # Cloudflare Worker backend
├── index.html # Chat UI (Cloudflare Pages)
├── schema.sql # D1 database schema
├── README.md # Project documentation
├── PROMPTS.md # AI prompts used
└── sample_data/ # Example ingested manual text


---

## How It Works

### Document Ingestion
- Manual text is split into overlapping chunks
- Each chunk is stored in D1 with:
  - `docId`
  - `chunkIndex`
  - `pageStart` / `pageEnd`
  - raw text

### Question Answering
1. User submits a question
2. Keywords are extracted from the question
3. D1 is queried using `LIKE` matching
4. Top-ranked chunks are selected
5. The system:
   - Returns retrieved excerpts directly **or**
   - Sends them to Workers AI for synthesis
6. Citations are returned with every answer

---




