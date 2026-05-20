# Scientific PDF RAG Pipeline

A Retrieval-Augmented Generation (RAG) pipeline for processing scientific PDF documents, generating embeddings, storing vectors in FAISS, and querying the knowledge base using a local LLM with Ollama.

---

## Overview

This notebook demonstrates a complete end-to-end RAG workflow:

1. Extract text and structured elements from PDF files.
2. Chunk and preprocess the extracted content.
3. Generate embeddings using Sentence Transformers.
4. Store embeddings in a FAISS vector database.
5. Retrieve relevant chunks using semantic similarity.
6. Query the knowledge base using a local LLM.

The project is focused on scientific research documents and technical PDFs.

---

## Features

* PDF ingestion using Unstructured.io
* OCR support for scanned PDFs
* Semantic chunking and document preprocessing
* Embedding generation using Sentence Transformers
* FAISS vector database for fast retrieval
* Max Marginal Relevance (MMR) retrieval
* Local LLM inference with Ollama
* Prompt-based RetrievalQA pipeline
* Persistent vector storage

---

## Tech Stack

### Core Libraries

* Python
* Jupyter Notebook
* LangChain
* FAISS
* Sentence Transformers
* Ollama
* Unstructured.io

### Models

* Embedding Model: `multilingual-e5-large`
* LLM: `llama3.1:8b` (via Ollama)

---

## Project Workflow

### 1. PDF Ingestion

The notebook uses the Unstructured ingestion pipeline to:

* Read PDF files from a local directory
* Extract text and document elements
* Handle scanned PDFs using OCR
* Store parsed outputs in JSON format

---

### 2. Chunking and Preprocessing

Extracted content is converted into LangChain `Document` objects.

The notebook then:

* Cleans the extracted text
* Splits large documents into smaller chunks
* Preserves metadata for retrieval

---

### 3. Embedding Generation

Embeddings are generated using Sentence Transformers.

These embeddings convert text chunks into dense vector representations for semantic search.

---

### 4. Vector Database Creation

The embeddings are stored in a FAISS vector database.

The database is persisted locally for reuse without rebuilding embeddings every time.

Example:

```python
FAISS.save_local("./db/vector_store")
```

---

### 5. Semantic Retrieval

The notebook performs similarity search using:

* Cosine similarity
* Max Marginal Relevance (MMR)

This helps retrieve the most relevant chunks while reducing redundancy.

---

### 6. LLM Question Answering

A RetrievalQA chain is created using:

* Ollama LLM
* FAISS retriever
* Custom prompt template

The model answers questions strictly based on retrieved context.

---

## Folder Structure

```text
project/
│
├── parsed_pdfs/           # Parsed JSON outputs
├── db/
│   └── vector_store/      # FAISS index and metadata
├── pdfs/                  # Input PDF documents
├── pipeline.ipynb         # Main notebook
└── README.md
```

---

## Installation

### Clone Repository

```bash
git clone https://github.com/AyushG-upta/RAG-Pipeline.git
cd RAG-Pipeline
```

---

### Create Virtual Environment

```bash
python -m venv venv
```

Activate environment:

#### Windows

```bash
venv\Scripts\activate
```

#### Linux / macOS

```bash
source venv/bin/activate
```

---

### Install Dependencies

```bash {for windows: poppler-utils and tesseract-ocr should be downloaded and must be added to the PATH}
pip install unstructured
pip install unstructured-ingest
pip install "unstructured[pdf]"
pip install poppler-utils
pip install tesseract-ocr
pip install langchain-community
pip install langchain-classic
pip install sentence-transformers
pip install faiss-cpu
pip install langchain-ollama
```
---

## Ollama Setup

Install Ollama from:

Ollama Official Website[https://ollama.com](https://ollama.com)

Pull the required model:

```bash
ollama pull llama3.1:8b
```

Run the model:

```bash
ollama run llama3.1:8b
```

---

## Running the Notebook

Start Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
pipeline.ipynb
```

Run all cells sequentially.

---

## Example Query

```python
query = "What is hardness in glass and how is it measured?" or "Describe about this Document-<document name>{uploaded in the dir}"
```

The system retrieves relevant chunks from the vector database and generates an answer using the LLM.

---

## Retrieval Strategy

The retriever uses:

```python
search_type = "mmr"
```

Benefits:

* Better diversity in retrieved chunks
* Reduced repetitive context
* Improved answer quality

---

## Future Improvements

Possible future enhancements:

* PostgreSQL or ChromaDB integration
* Hybrid search (BM25 + Vector Search)
* Multi-document summarization
* Metadata filtering
* Reranking models
* API deployment using FastAPI
* Frontend chatbot interface
* GPU acceleration
* Streaming responses

---

## Use Cases

* Scientific research assistants
* Academic paper search systems
* Technical document Q&A
* Knowledge retrieval systems
* Internal enterprise document assistants

---

## Notes

* FAISS indexes are stored locally.
* Large embedding models may require significant RAM.
* OCR quality depends on PDF scan quality.
* Ollama should be running locally before querying.

---

## License

This project is open-source and available under the MIT License.

---

## Author

Aayush Gupta

---

## Acknowledgements

* LangChain
* Unstructured.io
* FAISS
* Sentence Transformers
* Ollama
* Meta Llama
