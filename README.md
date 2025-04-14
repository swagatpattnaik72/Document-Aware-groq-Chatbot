# Groq-Powered Sherlock Holmes Chatbot

Document Used: The Adventures of Sherlock Holmes by Arthur Conan Doyle (Public Domain via Project Gutenberg)(https://www.gutenberg.org/ebooks/1661)

# Objective

This project builds an intelligent AI chatbot using Groq AI that can understand, summarize, and interact with a long-form document (in this case, The Adventures of Sherlock Holmes). The chatbot allows users to ask natural-language questions and receive accurate, context-aware, and well-cited answers.

# Architecture Overview

1. Text File Upload
   - Split into chunks (~500 tokens each)
2. Sentence Embedding
   - Using MiniLM (sentence-transformers) to embed text chunks
3. FAISS Vector Indexing
   - Store and index chunk embeddings for efficient retrieval
4. Query Input
   - User asks a question
5. Top-k Chunk Retrieval
   - Most relevant chunks retrieved from vector index
6. Prompt Construction
   - Combine retrieved chunks + user query into a single prompt
7. Groq LLM (LLaMA3-8B-8192)
   - Generate an intelligent response with:
       - Citations
       - Summarization
       - Simplified answers (ELI5)
8. Response Display
   - Show final answer and evaluation score

### Tools & Technologies Used

| Component                | Tool/Library                        | Purpose                                                  |
|--------------------------|-------------------------------------|----------------------------------------------------------|
| LLM Backend              | Groq AI (LLaMA3-8B-8192)            | Fast and efficient LLM-based responses                  |
| Document Format          | `.txt`                              | Long-form fictional novel                               |
| Embedding Model          | sentence-transformers (MiniLM)      | Generate semantic vector embeddings                     |
| Vector Store             | FAISS                               | For fast top-k similarity search                        |
| Interface                | Google Colab (Notebook UI)          | Interactive chatbot interface                           |
| Evaluation               | scikit-learn & Cosine Similarity    | Score model response vs. ground truth                   |
| Memory                   | Manual conversation history         | For multi-turn interaction memory                       |

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
   - Summarization on demand
   - "Explain like I'm 5" mode
   - Persona Mode (Sherlock Holmes style)
   - Evaluation Metrics with Faithfulness & Citation scores

# Evaluation Metrics

Each response is evaluated using:
- Faithfulness Score (0–10): Based on cosine similarity with a reference answer
- Citation Score (0 or 10): Based on whether proper chunk references were included
- Overall Score = (Faithfulness + Citation) / 2

# Sample Queries for Testing

1. Who is Irene Adler?
2. What is the story "A Scandal in Bohemia" about?
3. Who hired Sherlock Holmes in the Red-Headed League?
4. Explain like I'm 5: Who is Sherlock Holmes?
5. Summarize The Blue Carbuncle

# How to Run

1. Open the Google Colab notebook (see link below)
2. Upload the Sherlock Holmes text file
3. Follow each step cell-by-cell from installation to interaction
4. Use the chatbot via ask_chatbot("your question")

# Resources

- Document: The Adventures of Sherlock Holmes – Project Gutenberg
- Notebook: Colab Notebook Link (https://colab.research.google.com/drive/1wePHsry_54V3aa7c7JjYvhbRiMYzKhCZ#scrollTo=oTJJEsePycak)
- Groq API: Groq Cloud

# Reasoning Behind Choices

1. Groq AI was chosen for its ultra-fast, high-performance LLM capabilities.
2. FAISS + MiniLM enables efficient and compact semantic search over long documents.
3. The modular design (chunking → embedding → retrieval → prompt building → LLM) ensures flexibility, scalability, and multi-mode extensions like simplification, summarization, and persona.
4. Citation and evaluation metrics provide transparency and measurable reliability.

# Bonus Features Implemented

- Summarization on demand
- Explain Like I’m 5 mode
- Persona Mode (Sherlock style)
- Evaluation Scoring Function
- Proper source referencing (chunk citations)
- Multi-turn memory support
