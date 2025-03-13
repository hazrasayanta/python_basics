Here’s a **Retrieval Augmented Generation (RAG) project demo** using **FAISS for retrieval** and  **OpenAI’s GPT for response generation** .

---

# **🚀 RAG Chatbot: Fetching and Answering Questions from Documents**

### **Tech Stack:**

✅ **FAISS** - Vector-based retrieval

✅ **OpenAI GPT-4** - Response generation

✅ **Sentence Transformers** - Embedding generation

✅ **Flask** - API interface

---

## **📌 Project Structure**

```
rag-chatbot/
│── data/
│   ├── documents.txt   # Knowledge base
│── app.py              # Flask API for chatbot
│── retriever.py        # FAISS-based retrieval
│── generator.py        # OpenAI GPT-4 response generation
│── requirements.txt    # Dependencies
│── config.py           # API keys and settings
```

---

## **1️⃣ Install Dependencies**

```bash
pip install faiss-cpu sentence-transformers openai flask
```

---

## **2️⃣ Load and Embed Documents**

🔹 **Convert documents into vector embeddings for retrieval.**

### **📄 `retriever.py` (FAISS Indexing)**

```python
import faiss
import numpy as np
from sentence_transformers import SentenceTransformer

# Load the embedding model
model = SentenceTransformer('all-MiniLM-L6-v2')

# Load documents
with open("data/documents.txt", "r") as file:
    documents = file.readlines()

# Convert documents into embeddings
document_embeddings = model.encode(documents)

# Create FAISS index
dimension = document_embeddings.shape[1]
index = faiss.IndexFlatL2(dimension)
index.add(np.array(document_embeddings))

# Save index
faiss.write_index(index, "faiss_index.bin")

# Store document mapping
with open("doc_mapping.txt", "w") as f:
    for i, doc in enumerate(documents):
        f.write(f"{i}\t{doc.strip()}\n")

print("✅ FAISS Index Created & Saved!")
```

---

## **3️⃣ Retrieve Relevant Documents**

🔹 **Find the most relevant documents based on user queries.**

### **📄 `retriever.py` (Search Function)**

```python
def retrieve_documents(query, top_k=2):
    index = faiss.read_index("faiss_index.bin")
    query_embedding = model.encode([query])

    # Search for similar vectors
    distances, indices = index.search(query_embedding, top_k)

    # Get document text
    retrieved_docs = []
    with open("doc_mapping.txt", "r") as f:
        doc_mapping = {int(line.split("\t")[0]): line.split("\t")[1] for line in f}
  
    for idx in indices[0]:
        retrieved_docs.append(doc_mapping.get(idx, ""))

    return retrieved_docs
```

---

## **4️⃣ Generate Responses with OpenAI**

🔹 **Use retrieved documents as context for GPT.**

### **📄 `generator.py`**

```python
import openai
from config import OPENAI_API_KEY

openai.api_key = OPENAI_API_KEY

def generate_response(query, retrieved_docs):
    context = " ".join(retrieved_docs)
    prompt = f"Context: {context}\n\nAnswer this question: {query}"

    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}],
        max_tokens=150
    )

    return response["choices"][0]["message"]["content"]
```

---

## **5️⃣ Build a Chatbot API with Flask**

🔹 **Create an API endpoint to handle queries.**

### **📄 `app.py`**

```python
from flask import Flask, request, jsonify
from retriever import retrieve_documents
from generator import generate_response

app = Flask(__name__)

@app.route("/ask", methods=["POST"])
def ask():
    data = request.json
    query = data.get("query", "")

    retrieved_docs = retrieve_documents(query)
    response = generate_response(query, retrieved_docs)

    return jsonify({"query": query, "retrieved_docs": retrieved_docs, "response": response})

if __name__ == "__main__":
    app.run(debug=True)
```

---

## **6️⃣ Run the API**

```bash
python app.py
```

---

## **7️⃣ Test the RAG Chatbot**

Send a **POST request** to the API with a question.

### **Using cURL**

```bash
curl -X POST "http://127.0.0.1:5000/ask" -H "Content-Type: application/json" -d '{"query": "What is RAG?"}'
```

### **Expected JSON Response:**

```json
{
  "query": "What is RAG?",
  "retrieved_docs": ["RAG combines retrieval and generation to improve AI responses."],
  "response": "Retrieval Augmented Generation (RAG) combines document retrieval with language model generation to enhance accuracy and reduce hallucinations."
}
```

---

## **🚀 Features & Optimizations**

✅ **Retrieves relevant documents before generating answers.**

✅ **Uses FAISS for fast vector search.**

✅ **Connects OpenAI GPT-4 for high-quality responses.**

✅ **Exposes a REST API for easy integration.**

✅ **Can scale with Pinecone, Weaviate, or Milvus for production.**
