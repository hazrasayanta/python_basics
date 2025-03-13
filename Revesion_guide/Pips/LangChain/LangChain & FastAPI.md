Here’s a **LangChain + FastAPI project** where we build an **AI-powered chatbot** that uses LangChain’s **LLM capabilities and Retrieval-Augmented Generation (RAG)** to provide intelligent responses.

---

# **🚀 Project: AI Chatbot with LangChain & FastAPI**

✅ **Uses OpenAI’s GPT Model**

✅ **Includes RAG (Retrieval-Augmented Generation)**

✅ **Implements API Endpoints using FastAPI**

✅ **Supports File Uploads & Knowledge Retrieval**

---

## **1️⃣ Install Dependencies**

```bash
pip install fastapi uvicorn langchain openai faiss-cpu python-multipart
```

---

## **2️⃣ Project Structure**

```
📂 langchain_chatbot
 ┣ 📂 data/                # Stores knowledge base documents
 ┣ 📜 main.py              # FastAPI server
 ┣ 📜 chatbot.py           # LangChain implementation
 ┣ 📜 requirements.txt
```

---

## **3️⃣ LangChain Chatbot Logic (chatbot.py)**

This file handles **LLM processing, document retrieval, and chatbot responses.**

```python
from langchain.chat_models import ChatOpenAI
from langchain.vectorstores import FAISS
from langchain.embeddings.openai import OpenAIEmbeddings
from langchain.document_loaders import TextLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter
import os

# Set OpenAI API Key
os.environ["OPENAI_API_KEY"] = "your-api-key"

# Load documents
def load_documents(file_path):
    loader = TextLoader(file_path)
    documents = loader.load()
  
    # Split text into chunks
    text_splitter = RecursiveCharacterTextSplitter(chunk_size=500, chunk_overlap=50)
    docs = text_splitter.split_documents(documents)
  
    return docs

# Create vector database
def create_vector_db(file_path):
    docs = load_documents(file_path)
    vector_db = FAISS.from_documents(docs, OpenAIEmbeddings())
    return vector_db

# Initialize ChatBot with Retrieval
class Chatbot:
    def __init__(self, knowledge_base):
        self.llm = ChatOpenAI(model="gpt-3.5-turbo")
        self.vector_db = create_vector_db(knowledge_base)
  
    def ask(self, query):
        retriever = self.vector_db.as_retriever()
        docs = retriever.get_relevant_documents(query)
        context = " ".join([doc.page_content for doc in docs])
      
        prompt = f"Context: {context}\n\nUser: {query}\nAI:"
        response = self.llm.invoke(prompt)
      
        return response

# Initialize Chatbot with sample knowledge base
chatbot = Chatbot("data/knowledge.txt")
```

---

## **4️⃣ FastAPI Server (main.py)**

Creates API endpoints for chatbot interaction and file uploads.

```python
from fastapi import FastAPI, UploadFile, File, Form
from chatbot import chatbot

app = FastAPI()

@app.post("/ask/")
async def ask_question(query: str = Form(...)):
    response = chatbot.ask(query)
    return {"response": response}

@app.post("/upload/")
async def upload_knowledge(file: UploadFile = File(...)):
    file_path = f"data/{file.filename}"
    with open(file_path, "wb") as buffer:
        buffer.write(await file.read())

    chatbot.__init__(file_path)  # Reload chatbot with new data
    return {"message": "Knowledge base updated!"}
```

---

## **5️⃣ Running the FastAPI Server**

Start the API using Uvicorn:

```bash
uvicorn main:app --reload
```

---

## **6️⃣ Testing the API**

### **✔ Ask a Question**

```bash
curl -X POST "http://127.0.0.1:8000/ask/" -F "query=What is LangChain?"
```

✅ **Response:**

```json
{"response": "LangChain is a framework for building LLM-powered applications."}
```

### **✔ Upload New Knowledge**

```bash
curl -X POST "http://127.0.0.1:8000/upload/" -F "file=@new_knowledge.txt"
```

✅ **Response:**

```json
{"message": "Knowledge base updated!"}
```

---

## **🔹 Next Steps**

Would you like me to add  **JWT authentication** ,  **Dockerization** , or a **Frontend (React.js)** for this project? 🚀
