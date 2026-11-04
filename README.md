# Enterprise Document QA System (PDF-RAG)

An enterprise-ready **Retrieval-Augmented Generation (RAG)** pipeline that allows users to ask natural language questions against complex PDF documents and receive precise, context-bounded answers. Built using **LangChain**, **Google Gemini AI**, and **FAISS Vector Store**.

---

## 📌 Features

- **Automated PDF Ingestion:** Extracts, processes, and chunks complex PDF content.
- **Vector Search & Indexing:** Embeds document chunks using Google's `gemini-embedding-001` model and indices them locally using **FAISS** for fast similarity retrieval.
- **Strict Context-Bounded QA:** Leverages custom system prompts with **Google Gemini** (`gemini-3.5-flash-lite`) to ensure answers are derived strictly from the uploaded document, preventing hallucinations.
- **Persistent Indexing:** Checks for existing vector databases on startup to eliminate redundant document re-processing.

---

## 🛠️ Tech Stack

- **Language:** Python 3.10+
- **LLM & Embeddings:** Google Gemini API (`langchain-google-genai`)
- **Orchestration Framework:** LangChain (`langchain-core`, `langchain-community`)
- **Vector Database:** FAISS (`faiss-cpu`)
- **PDF Parser:** PyPDF (`pypdf`)
- **Environment Management:** Python-Dotenv (`python-dotenv`)

---

## 🏗️ Architecture Overview

```text
[ Document Input (.pdf) ]
          │
          ▼
 [ PyPDFLoader & Splitter ]  ──► (Chunks text into 800 chars / 100 overlap)
          │
          ▼
 [ Gemini Embeddings API ]    ──► (Generates vector embeddings)
          │
          ▼
 [ FAISS Vector Index ]      ──► (Stores & performs similarity search)
          │
          ▼
 [ User Query ] ──► [ Top-K Retrieval (k=3) ] ──► [ Prompt + Context ] ──► [ Gemini LLM ] ──► [ Output ]
```

---

## 🚀 Getting Started

### 1. Prerequisites

Make sure you have Python installed (v3.10 or higher recommended) and a Google Gemini API Key.

### 2. Installation

Clone the repository and navigate to the project root:

```bash
git clone https://github.com/YOUR_USERNAME/enterprise-doc-qa.git
cd enterprise-doc-qa
```

Install the required packages:

```bash
pip install -r requirements.txt
```

### 3. Environment Configuration

Create a `.env` file in the project root directory and add your API key:

```env
GOOGLE_API_KEY=your_gemini_api_key_here
```

### 4. Running the Application

Place your target PDF file (e.g., `Nexus Cloud Systems.pdf`) into the project root directory, then run the notebook or script:

```bash
jupyter notebook Chatbot.ipynb
```

---

## 📁 Project Structure

```text
enterprise-doc-qa/
│
├── Chatbot.ipynb              # Your main Jupyter Notebook implementation
├── requirements.txt           # Python package dependencies
├── README.md                  # Project documentation
├── .env                       # Environment variables (API keys - DO NOT push to GitHub)
├── .gitignore                 # Excludes faiss_index/ and .env
│
├── ABC_Company_Knowledge.pdf    # 📄 Your source data file (PDF)
│
└── faiss_index/               # 🗄️ Automatically generated vector database folder
    ├── index.faiss
    └── index.pkl

---

## 🔒 Security & Privacy

- **API Security:** Environment variables are used for credential handling (`.env`). API keys are never hardcoded or committed to version control.
- **Local Indexing:** Vector indices generated via FAISS are stored locally on your filesystem.

---
