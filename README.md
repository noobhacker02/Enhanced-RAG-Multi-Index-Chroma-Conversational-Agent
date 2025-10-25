# 🧠 Enhanced RAG + Multi-Index Chroma Conversational Agent

A **conversational AI system** combining **Retrieval-Augmented Generation (RAG)** with **Google Gemini**, **LangChain**, and **Chroma** for multi-domain document intelligence.

This agent can process PDFs, store them in persistent vector databases by domain, and answer queries using both retrieved context and tools — all while maintaining **persistent chat memory** across sessions.

---

## 🚀 Features

- **🧩 Multi-domain Chroma Vector Store**
  - Persistent storage with separate collections for each domain.
  - Incremental indexing with duplicate detection.

- **💬 Retrieval-Augmented Generation (RAG)**
  - Uses Google Gemini (`ChatGoogleGenerativeAI`) for context-aware answers.
  - Includes a query rewriting chain to improve search accuracy.

- **🧠 Persistent Memory**
  - Conversation history is stored in a JSON file and automatically loaded on startup.

- **🛠️ Built-in Tools**
  - **Calculator** for arithmetic queries.
  - **RAGRetriever** for document-based question answering.

- **📄 Rich Metadata**
  - Each document chunk stores `source`, `page`, `chunk`, and `domain` metadata.

- **🧮 CLI Interface**
  - Interactive terminal with options to upload PDFs, list stored files, ask questions, and manage memory.

---

## 🧰 Requirements

### Python
- Python 3.10 or later

### Install Dependencies
```bash
pip install langchain langchain-google-genai chromadb sentence-transformers PyMuPDF python-dotenv
````

### Environment Variables

Create a `.env` file in your project root:

```bash
GOOGLE_API_KEY=your_google_api_key_here
GEMINI_MODEL=gemini-2.0-flash
EMBEDDING_MODEL=sentence-transformers/all-MiniLM-L6-v2
```

---

## ⚙️ Setup & Run

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/enhanced-rag-agent.git
cd enhanced-rag-agent
```

### 2. Run the Script

```bash
python main.py
```

You’ll see the CLI menu:

```
1) Upload PDFs to index
2) List indexed PDFs
3) Ask a question (Agent handles RAG/Tools/Chat)
4) Run example queries
5) Clear Memory
6) Exit
```

---

## 🧾 How It Works

### 1. **PDF Ingestion**

* Select PDFs using a file picker.
* Text is extracted, split into overlapping chunks, and stored in Chroma with embeddings.
* Domains are detected automatically (e.g., `finance`, `legal`, `research`).

### 2. **Incremental Indexing**

* The system hashes each PDF to detect updates.
* If a file is unchanged, it’s skipped to save time.

### 3. **Retrieval-Augmented Generation (RAG)**

* On each question:

  1. Query is rewritten for clarity.
  2. Relevant chunks are retrieved from the matching domain.
  3. Gemini generates a grounded response using only that context.

### 4. **Memory**

* Every conversation turn is stored in `conversation_history.json`.
* When relaunched, the agent continues from previous sessions.

---

## 📚 Domain Mapping

| Domain       | Keywords                                       |
| ------------ | ---------------------------------------------- |
| **legal**    | law, contract, agreement, court, legal         |
| **finance**  | invoice, payment, finance, budget, tax         |
| **research** | chapter, study, research, methodology, results |
| **general**  | fallback for uncategorized content             |

---

## 🧮 Tools Overview

| Tool             | Description                                      |
| ---------------- | ------------------------------------------------ |
| **Calculator**   | Evaluates safe mathematical expressions          |
| **RAGRetriever** | Answers questions using indexed document content |

---

## 🧑‍💻 Example Queries

```text
Hi, my name is Alex.
What is 25 * 6?
Summarize the uploaded research paper.
What was my previous question?
```

---

## 📂 Project Structure

```
.
├── main.py                     # Main application file
├── chroma_db/                  # Vector database directory
├── conversation_history.json    # Persistent chat memory
├── pdf_cache.json               # Hash cache for PDFs
├── requirements.txt             # Python dependencies
└── .env                         # Environment variables
```

---

## 🧼 Maintenance Commands

**Clear Memory**

```bash
rm conversation_history.json
```

**Delete Chroma Database**

```bash
rm -rf chroma_db/
```

---

## ⚠️ Notes

* Make sure your **Google API key** has access to the Gemini model.
* The system avoids hallucination by grounding responses strictly to context.
* Persistent memory ensures continuity across restarts.

---

## 📜 License

This project is licensed under the **MIT License** — you can use, modify, and distribute it freely.

---

## 🤝 Contributing

Pull requests and improvements are welcome!
If you find a bug or want to extend features (e.g., new tools, APIs, or domain detection), feel free to open an issue.

---

### 💡 Future Enhancements

* Add vector-based summarization.
* Implement embedding caching.
* Integrate web document and YouTube transcript loaders.
* Deploy as a web app using Streamlit or Gradio.

---

**Author:** Talha Shaikh
**Tech Stack:** Python • LangChain • Chroma • Google Gemini • HuggingFace

```

---

Would you like me to include a matching **`requirements.txt`** and **`.env.example`** section (to make the repo plug-and-play for others)?
```
