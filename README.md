Enhanced RAG + Multi-Index Chroma Conversational Agent

A conversational AI agent built using LangChain, Chroma, and Google Gemini, capable of retrieval-augmented generation (RAG) across multiple domains with persistent memory. This agent can process PDFs, index them into domain-specific vector stores, and answer user queries using both indexed documents and tools like a calculator.

Features

Persistent Chroma Vector Store
Multi-collection, domain-specific storage for document embeddings. Incremental indexing with duplicate avoidance.

RAG with Google Gemini
Uses ChatGoogleGenerativeAI for LLM-based responses enhanced with relevant document context.

Persistent Conversation Memory
Stores chat history in a JSON file to maintain continuity across sessions.

Tools Integration

Calculator for arithmetic queries.

RAGRetriever for document-based question answering.

Metadata-rich Documents
PDF chunks are stored with metadata including source, page, chunk, and domain.

Query Rewriter Chain
Rewrites user queries for better retrieval results.

Hybrid Retrieval
Combines vector similarity search and keyword matching for robust document retrieval.

CLI Interface
Interactive menu to upload PDFs, list indexed documents, ask questions, and manage memory.

Requirements

Python 3.10+

Packages:

pip install langchain langchain-google-genai chromadb sentence-transformers PyMuPDF python-dotenv


Environment Variables
Create a .env file with the following keys:

GOOGLE_API_KEY=<your_google_api_key>
GEMINI_MODEL=gemini-2.0-flash
EMBEDDING_MODEL=sentence-transformers/all-MiniLM-L6-v2

Installation

Clone this repository:

git clone <repo_url>
cd <repo_folder>


Install dependencies:

pip install -r requirements.txt


Set up .env with your Google API key and optional model names.

Usage

Run the conversational agent:

python main.py


You will see the CLI menu:

Upload PDFs to index – Select PDFs to split into chunks and index into Chroma.

List indexed PDFs – Shows all PDFs stored per domain.

Ask a question – Agent will handle RAG retrieval, tools, and memory-based answers.

Run example queries – Quick demonstration queries to test agent capabilities.

Clear Memory – Resets persistent conversation history.

Exit – Quit the application.

PDF Processing & Indexing

PDFs are split into chunks with customizable chunk_size and chunk_overlap.

Metadata is stored for each chunk (source, page, chunk, domain).

Duplicate chunks are ignored during re-indexing.

Domain detection is automatic based on content keywords, or manually specified.

Tools

Calculator – Safely evaluates arithmetic expressions.

RAGRetriever – Answers questions using indexed document chunks.

Persistent Memory

Conversation history is stored in conversation_history.json.

Automatically loaded at startup and saved after each interaction.

Memory is shared with the agent for context-aware responses.

Domain Mapping (Default)
Domain	Keywords
legal	law, contract, agreement, court, legal
finance	invoice, payment, finance, budget, tax
research	chapter, study, research, methodology, results
general	fallback domain for unmatched content
Example Queries

Hi, my name is Alex.

What is 25*6?

Summarize the main points from the uploaded PDF on finance.

The agent uses both tools and RAG to provide accurate, context-aware answers.

File Structure
.
├── main.py                  # Entry point for the agent CLI
├── conversation_history.json # Persistent memory storage
├── chroma_db/               # Chroma vector store directory
├── pdf_cache.json           # Tracks processed PDFs to avoid duplicates
├── requirements.txt         # Python dependencies
└── .env                     # API keys and model configs

Notes

Ensure your Google API key is valid and has access to Gemini.

Memory and vector store are persistent, allowing multi-session usage.

Incremental PDF indexing avoids reprocessing unchanged files.

License

MIT License – Feel free to use and modify.
