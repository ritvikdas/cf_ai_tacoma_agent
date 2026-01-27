# cf_ai_tacoma_agent

An AI-powered chat application built on **Cloudflare Workers, D1, and Pages** that allows users to ask natural-language questions about a Toyota Tacoma owner’s manual.  
The system performs document ingestion, keyword-based retrieval, and (optionally) LLM-based answer generation using Cloudflare Workers AI.

This project demonstrates how to build a lightweight Retrieval-Augmented Generation (RAG) style application entirely on Cloudflare’s edge platform.

---

## 🚀 Live Demo

**Chat UI (Cloudflare Pages):**  
https://cf-ai-tacoma-agent.pages.dev

**API Worker:**  
https://super-wood-6e6a.ritvik2.workers.dev

---

## 🧠 What This Project Does

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

## 🧩 Architecture Overview

