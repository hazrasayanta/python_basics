# **📌 LangChain Interview Guide with Hands-On Implementation**

## **🔹 What is LangChain?**

LangChain is a  **framework for developing applications powered by LLMs (Large Language Models)** , such as OpenAI’s GPT. It helps with:

✅ **Prompt Engineering**

✅ **Memory & Context Handling**

✅ **Tool & API Integrations**

✅ **Retrieval-Augmented Generation (RAG)**

✅ **Agents & Chains**

---

## **1️⃣ Installation**

```bash
pip install langchain openai
```

### **🔹 Optional Dependencies**

* `chromadb` → Vector database
* `faiss-cpu` → Fast indexing
* `python-dotenv` → Environment variables

```bash
pip install chromadb faiss-cpu python-dotenv
```

---

## **2️⃣ Basic LangChain Usage**

### **🔹 Setting Up OpenAI LLM**

```python
from langchain.chat_models import ChatOpenAI
import os

# Load API key from environment variables
os.environ["OPENAI_API_KEY"] = "your-api-key"

# Initialize LLM
llm = ChatOpenAI(model="gpt-3.5-turbo")

response = llm.invoke("What is LangChain?")
print(response)
```

---

## **3️⃣ Using Prompt Templates**

LangChain allows **dynamic prompt creation** using templates.

```python
from langchain.prompts import PromptTemplate

template = PromptTemplate.from_template("What are the benefits of {topic}?")
prompt = template.format(topic="LangChain")
print(prompt)
```

✅ **Output:**

```
What are the benefits of LangChain?
```

---

## **4️⃣ Chains – Combining Multiple Steps**

LangChain **chains** multiple LLM calls together.

```python
from langchain.chains import LLMChain

llm_chain = LLMChain(llm=llm, prompt=template)
response = llm_chain.run("LangChain")
print(response)
```

---

## **5️⃣ Memory – Maintaining Conversation Context**

Memory helps  **LLMs remember previous interactions** .

```python
from langchain.memory import ConversationBufferMemory
from langchain.chains import ConversationChain

memory = ConversationBufferMemory()
conversation = ConversationChain(llm=llm, memory=memory)

response1 = conversation.run("Who won the FIFA World Cup in 2022?")
response2 = conversation.run("Which country hosted it?")
print(response1, response2)
```

---

## **6️⃣ Retrieval-Augmented Generation (RAG)**

RAG combines **LLMs with vector databases** for  **knowledge retrieval** .

```python
from langchain.vectorstores import FAISS
from langchain.embeddings.openai import OpenAIEmbeddings

documents = ["LangChain helps build LLM applications.", "RAG improves LLM accuracy."]
vectorstore = FAISS.from_texts(documents, OpenAIEmbeddings())

retriever = vectorstore.as_retriever()
retrieved_docs = retriever.get_relevant_documents("How does LangChain help?")
print(retrieved_docs)
```

---

## **7️⃣ Agents – Dynamic Task Execution**

Agents **decide** how to use tools dynamically.

```python
from langchain.agents import initialize_agent, AgentType
from langchain.tools import Tool

def multiply(x, y):
    return x * y

tool = Tool(name="Multiplication", func=multiply, description="Multiplies two numbers")

agent = initialize_agent([tool], llm, agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION, verbose=True)
response = agent.run("Multiply 5 by 3")
print(response)
```

---

## **🔹 Interview Questions**

### **1️⃣ Basic Questions**

✔ What is LangChain?

✔ Why use LangChain over direct OpenAI API calls?

✔ What are LangChain  **chains** , and how do they work?

### **2️⃣ Advanced Questions**

✔ Explain **RAG** and how it improves LLM responses.

✔ How does **LangChain memory** maintain conversation context?

✔ What are **Agents** in LangChain?
