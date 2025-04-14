# Groq-Powered Document-Aware Chatbot

Document Used: The Adventures of Sherlock Holmes by Arthur Conan Doyle (Public Domain via Project Gutenberg)(https://www.gutenberg.org/ebooks/1661)

# Objective

The goal of this project is to build an intelligent, high-performance Generative AI chatbot capable of understanding and interacting with a long-form document (100+ pages) using Groq AI. This solution supports contextual Q&A, summarization, citation-based answers, memory for multi-turn conversations, and evaluation metrics.

# Architecture Overview

<pre> ```mermaid graph LR A[Text File Upload] --> B[Chunking the Document] B --> C[Sentence Embedding (MiniLM)] C --> D[FAISS Vector Indexing] D --> E[Query Input] E --> F[Top-k Chunk Retrieval] F --> G[Prompt Construction with Context] G --> H[Groq LLM (LLaMA3-8B-8192)] H --> I[Answer Generation with Optional Citation / Summarization / Simplification] I --> J[Response Display + Evaluation Scoring] ``` </pre>

### Tools & Technologies Used

| Component                | Tool/Library                        | Purpose                                                  |
|--------------------------|-------------------------------------|----------------------------------------------------------|
| 💬 LLM Backend           | Groq AI (LLaMA3-8B-8192)            | Fast and efficient LLM-based responses                  |
| 📄 Document Format       | `.txt`                              | Long-form fictional novel                               |
| 📐 Embedding Model       | sentence-transformers (MiniLM)      | Generate semantic vector embeddings                     |
| 📦 Vector Store          | FAISS                               | For fast top-k similarity search                        |
| 🤖 Interface             | Google Colab (Notebook UI)          | Interactive chatbot interface                           |
| 📊 Evaluation            | scikit-learn & Cosine Similarity    | Score model response vs. ground truth                   |
| 🧠 Memory                | Manual conversation history         | For multi-turn interaction memory                       |

# Core Features

1. Document Chunking
Splits the 100+ page document into manageable text chunks (~500 tokens) for embedding and retrieval.
2. Sentence Embeddings
Uses all-MiniLM-L6-v2 from sentence-transformers to encode both document chunks and user queries.
3. Vector Search with FAISS
Indexes the document embeddings and retrieves the most relevant chunks for each user query.
4. Groq-Powered Q&A
Queries are answered using Groq’s LLaMA3 model by combining user input with retrieved context chunks.
5. Citation Support
Responses include citation references such as “(see Chunk 12)” to show the source text.

6. Special Modes
🔍 Summarization on demand
🧒 "Explain like I'm 5" mode
🧠 Persona Mode (Sherlock Holmes style)
📊 Evaluation Metrics with Faithfulness & Citation scores

# Evaluation Metrics

Each response is evaluated using:
Faithfulness Score (0–10): Based on cosine similarity with a reference answer
Citation Score (0 or 10): Based on whether proper chunk references were included
Overall Score = (Faithfulness + Citation) / 2

# Sample Queries for Testing

Who is Irene Adler?
What is the story "A Scandal in Bohemia" about?
Who hired Sherlock Holmes in the Red-Headed League?
Explain like I'm 5: Who is Sherlock Holmes?
Summarize The Blue Carbuncle

# How to Run

Open the Google Colab notebook (see link below)
Upload the Sherlock Holmes text file
Follow each step cell-by-cell from installation to interaction
Use the chatbot via ask_chatbot("your question")

# Resources

📘 Document: The Adventures of Sherlock Holmes – Project Gutenberg
📁 Notebook: Colab Notebook Link (Insert your actual Colab link here)
🤖 Groq API: Groq Cloud

# Reasoning Behind Choices

Groq AI was chosen for its ultra-fast, high-performance LLM capabilities.
FAISS + MiniLM enables efficient and compact semantic search over long documents.
The modular design (chunking → embedding → retrieval → prompt building → LLM) ensures flexibility, scalability, and multi-mode extensions like simplification, summarization, and persona.
Citation and evaluation metrics provide transparency and measurable reliability.

# Bonus Features Implemented

✅ Summarization on demand
✅ Explain Like I’m 5 mode
✅ Persona Mode (Sherlock style)
✅ Evaluation Scoring Function
✅ Proper source referencing (chunk citations)
✅ Multi-turn memory support
