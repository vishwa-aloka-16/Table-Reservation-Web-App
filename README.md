# ROSS AI

<p align="center">
  <a href="https://ross-ai.netlify.app/"><strong>Explore the Web App</strong></a>
  |
  <a href="https://github.com/vishwa-aloka-16/ross-webapp"><strong>Production Repository</strong></a>
</p>

---

## Live Deployment Notice

> **Performance Note:** ROSS is currently hosted utilizing free-tier infrastructure. If the application has been idle, backend services may require a brief initialization period. Please allow **30 to 50 seconds** upon your initial request for the server instances to spin up and respond properly.

---

## System Overview

ROSS is an AI-powered legal document analysis platform designed to ingest contracts and legal PDFs, generate hierarchical structured summaries, and provide document-grounded insights through an interactive chat interface. 

The architecture is split into three decoupled services:
* **`webapp/`** – A responsive React frontend optimized for user interaction.
* **`gateway/`** – A Node.js API layer managing authentication, document workflows, and service orchestration.
* **`ai-service/`** – A Python-based AI pipeline executing PDF ingestion, clustering, semantic tree generation, and retrieval-augmented generation (RAG).

---

## Key Features

* **Authentication & Document Tracking:** Secure user onboarding and comprehensive status tracking for uploaded files.
* **Automated Ingestion Pipeline:** Asynchronous text extraction and layout processing for dense legal documentation.
* **Hierarchical Summary Trees:** Structural aggregation of document sections to capture both high-level context and granular details.
* **Contextual Q&A:** RAG-driven conversational interface delivering responses strictly grounded in the document text, complete with precise citations.

---

## System Architecture

1. **Client Interaction:** The frontend transmits authenticated document uploads and API requests to the Central Gateway.
2. **Orchestration & Storage:** The gateway persists primary metadata in MongoDB, transfers the raw PDF binary to Supabase Storage, and dispatches an ingestion trigger to the AI Service.
3. **Semantic Processing:** The Python service extracts document structures, chunks content using layout-aware strategies, generates vector embeddings, and structures contextual nodes within a Postgres `pgvector` instance.
4. **Retrieval & Synthesis:** The user queries the system via the frontend, prompting the gateway to interface with the AI pipeline for vector similarity matching, summary generation, and LLM synthesis.

---

## Technical Specification

### Core Infrastructure & Models
* **Language Models & Embeddings:** Gemini API
* **Vector Database:** Supabase Postgres + `pgvector`
* **Metadata Store:** MongoDB Atlas
* **Object Storage:** Supabase Storage

### Frontend Service (`webapp/`)
* Runtime Framework: React 19 / Vite
* Rich Text Rendering: React Markdown / Remark GFM
* Code & Structure Highlighting: React Syntax Highlighter
* Interface Styling: Native CSS Architecture

### Application Gateway (`gateway/`)
* Engine: Node.js / Express
* Data Modeling: Mongoose
* Security: JSON Web Tokens (JWT) / BcryptJS
* File Processing: Multer
* Infrastructure Clients: Supabase JS SDK

### Intelligence Service (`ai-service/`)
* Engine: Python / Flask / Gunicorn
* Schema Validation: Pydantic v2 / Pydantic Settings
* Document Intelligence: PyPDF
* Mathematical & Clustering Utilities: NumPy / SciPy / Scikit-Learn
* Vector Operations: Psycopg 3 / pgvector-python
* Inference Engine: Google GenAI SDK

---

## Repository Structure

```text
ross-webapp/
├── webapp/           # React application layer
├── gateway/          # Node.js orchestration and API layer
├── ai-service/       # Python semantic processing pipeline
└── data/             # Local testing assets and document templates
