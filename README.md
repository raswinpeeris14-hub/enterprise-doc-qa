PDF RAG Chatbot — Enterprise Document QA AssistantA high-performance Retrieval-Augmented Generation (RAG) system designed to answer user queries based on the context extracted from enterprise PDF documents. Powered by LangChain, FAISS, and Google Gemini (Generative AI), this chatbot ensures accurate, context-grounded responses with minimal hallucination.Key FeaturesDocument Ingestion & Splitting: Loads and processes structured/unstructured PDF content using PyPDFLoader and intelligent RecursiveCharacterTextSplitter.Vector Search & Indexing: Generates document embeddings via GoogleGenerativeAIEmbeddings (gemini-embedding-001) and indexes them locally with FAISS for fast vector retrieval.Context-Grounded QA: Utilizes ChatGoogleGenerativeAI (gemini-3.5-flash-lite) configured with low temperature to ensure strict adherence to document facts.Interactive CLI Interface: Conversational loop that accepts user queries, retrieves relevant context chunks ($k=3$), and streams natural language responses.Tech Stack & DependenciesLanguage: Python 3.10+LLM Engine: Google Gemini API (ChatGoogleGenerativeAI, GoogleGenerativeAIEmbeddings)Orchestration Framework: LangChain (langchain-core, langchain-community, langchain-google-genai)Vector Database: FAISS (faiss-cpu)Document Parser: PyPDF (pypdf)Environment Management: Python-Dotenv (python-dotenv)Project Structure.
├── Chatbot.ipynb              # Main execution notebook / application workflow
├── requirements.txt           # Python dependencies
├── .env.example               # Template for required environment variables
├── Nexus Cloud Systems.pdf    # Sample input PDF document
├── faiss_index/               # Local persistence directory for FAISS index
└── README.md                  # Project documentation
Getting Started1. PrerequisitesEnsure you have Python 3.10 or higher installed, as well as a Google Gemini API key.2. Clone the Repositorygit clone https://github.com/YOUR_USERNAME/pdf-rag-chatbot.git
cd pdf-rag-chatbot
3. Set Up Virtual Environment & Install Dependencies# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
4. Configure Environment VariablesCreate a .env file in the root directory and add your Google Gemini API key:GOOGLE_API_KEY=your_gemini_api_key_here
UsagePlace the PDF document you want to query into the project root directory (e.g., Nexus Cloud Systems.pdf).Run the Chatbot.ipynb notebook or execute the script entry point:python -m jupyter notebook Chatbot.ipynb
Type your questions in the prompt. Type exit or quit to end the session.System Architecture & RAG Pipeline[ PDF Document ] ──► [ PyPDFLoader ] ──► [ Recursive Text Splitter ]
                                                    │
                                                    ▼
[ User Query ] ──► [ Gemini Embeddings ] ──► [ FAISS Vector Store ]
       │                                            │
       ▼                                            ▼
[ ChatPromptTemplate ] ◄────────────────── [ Top-k Relevant Chunks ]
       │
       ▼
[ ChatGoogleGenerativeAI ] ──► [ Answer / Output Parser ]
Indexing Phase:PDF pages are loaded and split into overlapping chunks (chunk_size=800, chunk_overlap=100).Vector representations are computed and cached in a local FAISS index (faiss_index/).Retrieval & Inference Phase:User input is embedded using the same vector space.Top 3 most relevant document chunks are retrieved via vector distance similarity.A constrained prompt forces the Gemini LLM to answer strictly using the retrieved context.LicenseThis project is open-source and available under the MIT License.
