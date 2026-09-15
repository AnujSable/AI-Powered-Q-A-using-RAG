# 📄 DocuRAG — Intelligent PDF Question Answering System

**DocuRAG** is an AI-powered document question-answering system built using **Retrieval-Augmented Generation (RAG)**.

It allows users to upload a PDF document, ask questions about its content, retrieve the most relevant information using semantic search, and generate context-aware answers using an LLM.

The goal of this project is to make it easier to interact with large PDF documents without manually searching through every page.

---

## 🚀 Features

- 📤 Upload PDF documents
- 📖 Extract text from PDF files
- ✂️ Split documents into smaller chunks
- 🧠 Generate semantic embeddings using Sentence Transformers
- 🔎 Perform semantic similarity search using ChromaDB
- 🤖 Generate answers using an OpenAI LLM
- 💬 Ask natural-language questions about uploaded documents
- 📚 Retrieve relevant document context before generating answers
- 🖥️ Streamlit-based user interface
- 🚫 Reduce unsupported answers by instructing the model to use document context only

---

## 🏗️ System Architecture

```text
                ┌─────────────────┐
                │    PDF Upload   │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │  PDF Text       │
                │  Extraction     │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Text Chunking   │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Sentence        │
                │ Transformer     │
                │ Embeddings      │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │    ChromaDB     │
                │  Vector Store   │
                └────────┬────────┘
                         │
                  User Question
                         │
                         ▼
                ┌─────────────────┐
                │ Query Embedding │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Semantic Search │
                │ Top-K Retrieval │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Relevant        │
                │ Context         │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │   OpenAI LLM    │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │  Final Answer   │
                └─────────────────┘
```

---

## 🧠 How RAG Works in This Project

DocuRAG follows a Retrieval-Augmented Generation workflow.

### 1. Document Ingestion

The user uploads a PDF document.

The system extracts the text from the PDF using **PyPDF**.

### 2. Text Chunking

Large documents are divided into smaller chunks.

This makes it easier to retrieve only the sections relevant to a user's question.

### 3. Embedding Generation

Each text chunk is converted into a numerical vector using:

```text
all-MiniLM-L6-v2
```

These vectors represent the semantic meaning of the text.

### 4. Vector Storage

The embeddings and corresponding document chunks are stored in **ChromaDB**.

### 5. Question Processing

When the user asks a question, the question is also converted into an embedding.

### 6. Semantic Retrieval

The system searches the vector database and retrieves the most semantically relevant document chunks.

### 7. Context Construction

The retrieved chunks are combined into a context provided to the language model.

### 8. Answer Generation

The LLM generates an answer based on the retrieved document context rather than searching the entire PDF manually.

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| PyPDF | PDF text extraction |
| Sentence Transformers | Text embeddings |
| ChromaDB | Vector database |
| OpenAI API | Answer generation |
| Streamlit | Web application interface |
| Jupyter Notebook | RAG pipeline development |

---

## 📁 Project Structure

```text
DocuRAG/
│
├── app.py
│
├── 11_RAG_pipeline.ipynb
│
├── data/
│   └── pdfs/
│       └── sample.pdf
│
├── .streamlit/
│   └── secrets.toml
│
├── requirements.txt
│
└── README.md
```

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/your-username/DocuRAG.git
```

Move into the project directory:

```bash
cd DocuRAG
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 🔑 API Key Configuration

DocuRAG uses the OpenAI API for generating answers.

Create:

```text
.streamlit/secrets.toml
```

Add:

```toml
OPENAI_API_KEY = "your-api-key"
```

### ⚠️ Security

Never commit your API key to GitHub.

Add this to `.gitignore`:

```text
.streamlit/secrets.toml
.env
venv/
__pycache__/
```

---

## ▶️ Run the Application

Start the Streamlit application:

```bash
streamlit run app.py
```

The application will open in your browser.

You can then:

```text
1. Upload a PDF
       ↓
2. Wait for processing
       ↓
3. Enter your question
       ↓
4. Retrieve relevant information
       ↓
5. Receive an AI-generated answer
```

---

## 💡 Example

### Uploaded Document

```text
Machine Learning.pdf
```

### Question

```text
What is supervised learning?
```

### System Process

```text
Question
   ↓
Query Embedding
   ↓
ChromaDB Search
   ↓
Relevant PDF Chunks
   ↓
LLM
   ↓
Answer
```

### Example Answer

```text
Supervised learning is a machine learning approach
where a model learns from labeled training data to
make predictions or decisions.
```

---

## 🎯 Project Objectives

The main objectives of DocuRAG are:

- Build a practical Retrieval-Augmented Generation pipeline
- Understand document ingestion and preprocessing
- Implement semantic search using vector embeddings
- Store and retrieve document knowledge using a vector database
- Connect retrieved context with an LLM
- Build an interactive document question-answering application
- Reduce the need for manual document searching

---

## 📊 RAG Pipeline Components

### Document Processing

```text
PDF → Text → Chunks
```

### Knowledge Representation

```text
Chunks → Embeddings → Vectors
```

### Retrieval

```text
Question → Query Embedding → Similarity Search → Top-K Chunks
```

### Generation

```text
Retrieved Context + Question → LLM → Answer
```

---

## 🔮 Future Improvements

The project can be further improved with:

- 🔄 Multi-PDF question answering
- 💬 Conversational chat history
- 📌 Page-level source citations
- 🎯 Improved retrieval and reranking
- 📊 RAG evaluation metrics
- 📈 Retrieval accuracy evaluation
- ⚡ Response-time optimization
- 🗂️ Document management
- 🔐 User authentication
- ☁️ Cloud deployment
- 🧹 Better document preprocessing
- 📑 Support for additional document formats
- 🧠 Hybrid keyword + semantic search

---

## 📌 Current Limitations

The current version is primarily designed as a learning and portfolio project.

Its answer quality depends on:

- Quality of extracted PDF text
- Chunk size and chunking strategy
- Embedding model
- Retrieval quality
- Number of retrieved chunks
- LLM response quality

Scanned/image-only PDFs may require OCR support for reliable text extraction.

---

## 🎓 Learning Outcomes

Through this project, I explored and implemented concepts including:

- Retrieval-Augmented Generation
- Natural Language Processing
- Text embeddings
- Semantic similarity
- Vector databases
- Document retrieval
- Prompt engineering
- LLM integration
- PDF processing
- Streamlit application development

---

## 👨‍💻 Author

**Anuj Sable**

Built as a practical AI/NLP project to explore **Retrieval-Augmented Generation, semantic search, vector databases, and LLM-powered document question answering**.

---

## ⭐ Project Summary

> **DocuRAG is an intelligent PDF question-answering system that combines document processing, semantic embeddings, vector search, and LLM-based generation to provide context-aware answers from uploaded documents.**

If you find this project useful, consider giving the repository a ⭐.