# 📂 RAG Chatbot for Company Documents using Google Drive and Gemini

A **Retrieval-Augmented Generation (RAG) Chatbot** built with  **n8n** ,  **Google Drive** ,  **Google Gemini** , and  **Pinecone** .

This project allows you to query your company documents stored in Google Drive. Documents are automatically indexed into **Pinecone** using  **Google Gemini embeddings** , and a conversational agent retrieves relevant context to provide precise, document-grounded answers.

---

## 🚀 Features

* 📁 **Google Drive Integration** → Watches specific folders for new/updated documents.
* 🔎 **RAG-powered Retrieval** → Uses Pinecone as a vector database.
* 🧠 **Google Gemini Embeddings** → Generates semantic embeddings for document chunks.
* 💬 **Conversational Agent** → Gemini-based chatbot with memory for smooth context-aware interactions.
* ⚡ **Automated Document Pipeline** → File ingestion, text splitting, embedding, and storage handled seamlessly in n8n.
* 🛠️ **Custom Tooling** → `company_documents_tool` retrieves document-based answers.

---

## 🏗️ Workflow Architecture

1. **Google Drive Triggers**
   * Detects **file creation** or **file updates** in a chosen folder.
2. **File Processing**
   * Downloads documents → Loads data → Splits into chunks.
3. **Embedding + Storage**
   * Generates embeddings with Google Gemini.
   * Stores vectors in  **Pinecone Vector Store** .
4. **Conversational Agent**
   * User query received → Retrieval from Pinecone.
   * Google Gemini Chat Model generates context-grounded response.
   * Maintains short-term memory via  **Window Buffer Memory** .

---

## ⚙️ Tech Stack

* **n8n** – Workflow automation engine
* **Google Drive API** – Document source
* **Google Gemini (PaLM API)** – Embeddings + LLM responses
* **Pinecone** – Vector database for semantic search
* **LangChain (via n8n nodes)** – RAG framework integration

---

## 📌 Prerequisites

Before using this workflow, set up the following:

* ✅ Google Drive account & API credentials
* ✅ Google Gemini (PaLM API) key
* ✅ Pinecone API key + active index
* ✅ n8n instance (self-hosted or cloud)

---

## 🛠️ Setup Instructions

1. Clone this repository:
   <pre class="overflow-visible!" data-start="2304" data-end="2426"><div class="contain-inline-size rounded-2xl relative bg-token-sidebar-surface-primary"><div class="sticky top-9"><div class="absolute end-0 bottom-0 flex h-9 items-center pe-2"><div class="bg-token-bg-elevated-secondary text-token-text-secondary flex items-center gap-4 rounded-sm px-2 font-sans text-xs"><span class="" data-state="closed"></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="whitespace-pre! language-bash"><span><span>git </span><span>clone</span><span> https://github.com/your-username/rag-chatbot-gdrive-gemini.git
   </span><span>cd</span><span> rag-chatbot-gdrive-gemini
   </span></span></code></div></div></pre>
2. Import the workflow JSON into your  **n8n instance** .
3. Configure the following **credentials** in n8n:
   * Google Drive OAuth2
   * Google Gemini (PaLM API)
   * Pinecone API
4. Update workflow variables (e.g., Google Drive folder ID, Pinecone index name).
5. Activate the workflow → The chatbot will now start processing documents and answering queries.

---

## 🖥️ Usage

* Upload or update a file in your configured  **Google Drive folder** .
* The file is automatically embedded and stored in Pinecone.
* Send a **chat message** to the agent (via n8n trigger or UI).
* The chatbot retrieves the most relevant context and provides an accurate answer.

If the answer cannot be found in documents, the bot responds with:

> *"I cannot find the answer in the available resources."*

---

## 📊 Example Use Cases

* Company policy or HR document queries
* Product manuals & technical documentation search
* Knowledge base support chatbot
* Internal compliance & SOP retrieval

---

## 📌 Roadmap

* [ ] Add support for multiple document types (PDF, Word, etc.)
* [ ] Enable multi-user chat sessions with memory isolation
* [ ] Deploy as a standalone chatbot web app

---

## 🤝 Contributing

Contributions are welcome!

Please open an **issue** or submit a **pull request** for improvements.
