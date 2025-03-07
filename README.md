# PDF-based Chatbot

## Overview
This project is a **PDF-based chatbot** that leverages **FAISS (Facebook AI Similarity Search), Sentence Transformers, DeepSeek-LLM, and Gradio** to enable users to ask questions and receive responses based on the content of a given PDF document.

## Features
- **Extracts text from PDFs** using `PyPDFLoader`
- **Splits text into smaller chunks** for better retrieval
- **Embeds text** using `SentenceTransformer`
- **Uses FAISS for efficient similarity search**
- **Generates accurate answers** with `DeepSeek-LLM`
- **Provides an interactive chatbot** with `Gradio`

---

## **Project Workflow**

### **Step 1: Initialize DeepSeek LLM Model**
- Load the `DeepSeek-V3` model via **Hugging Face Hub**.
- Set model parameters for optimal response generation.

### **Step 2: Load and Extract Text from a PDF**
- Load the **PDF document** and extract text using `PyPDFLoader`.

### **Step 3: Split Text into Chunks**
- **Break down the extracted text** into smaller **overlapping chunks**.
- This improves retrieval and **preserves context**.

### **Step 4: Convert Text Chunks into Embeddings**
- Use **Sentence Transformers (`all-MiniLM-L6-v2`)** to convert each text chunk into a **numerical embedding (vector)**.
- These embeddings store meaning and allow efficient similarity search.

### **Step 5: Build and Save FAISS Index**
- Store embeddings in a **FAISS index** for fast similarity searches.
- Creates an L2 (Euclidean Distance) FAISS Index.
- Save the index to disk for reuse.

### **Step 6: Load FAISS Index (If Exists)**
- If an index already exists, **load it instead of rebuilding**.

### **Step 7: Search for Relevant Chunks in FAISS**
- Perform **similarity search** using FAISS to find the **most relevant text chunks** for a given query.
- Finds text chunks similar to the query using FAISS nearest neighbor search.
- Uses cosine similarity (inverted Euclidean distance) for ranking.


### **Step 8: Generate Answer Using DeepSeek-LLM**
- Use **retrieved context** from FAISS to **construct a prompt**.
- Pass the prompt to **DeepSeek-LLM** for generating an **accurate response**.

### **Step 9: Load PDF and Process it**
- The script **automatically processes** the PDF and creates embeddings if needed.
- Loads the FAISS index for efficient searching.

### **Step 10: Create Gradio Chatbot**
- Use `Gradio` to create a **simple chatbot UI**.
- Users can interact by **asking questions**, and the chatbot **retrieves relevant answers**.

---
