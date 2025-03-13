# 🚀 **FastAPI Hands-on Project Ideas** 🚀

Here are some **practical projects** to help you gain hands-on experience with FastAPI. Each project idea includes  **key features** ,  **technologies used** , and  **implementation steps** .

---

## **1️⃣ CRUD API with FastAPI & PostgreSQL**

**🔹 Features:**

✅ User authentication (JWT-based).

✅ CRUD operations for users & items.

✅ PostgreSQL as the database.

✅ Pydantic models for validation.

✅ Swagger UI for testing.

### **📄 Tech Stack**

* **FastAPI** (for API development).
* **PostgreSQL** (for data storage).
* **SQLAlchemy** (for ORM).
* **JWT authentication** (OAuth2).

### **🛠️ Steps to Build**

1. **Setup FastAPI & PostgreSQL**
   ```bash
   pip install fastapi uvicorn sqlalchemy psycopg2 pydantic
   ```
2. **Create a Database Model** (`models.py`)
   ```python
   from sqlalchemy import Column, Integer, String, Boolean
   from database import Base

   class User(Base):
       __tablename__ = "users"
       id = Column(Integer, primary_key=True, index=True)
       name = Column(String, index=True)
       email = Column(String, unique=True, index=True)
       password = Column(String)
   ```
3. **Setup CRUD Operations** (`crud.py`)
4. **Build Authentication with JWT** (`auth.py`).
5. **Test API using Swagger UI (`/docs`).**

---

## **2️⃣ AI-Powered Chatbot API**

**🔹 Features:**

✅ Accepts user queries via API.

✅ Uses OpenAI's GPT API or a local LLM model.

✅ Stores conversation history.

✅ Returns AI-generated responses.

### **📄 Tech Stack**

* **FastAPI** (API development).
* **OpenAI API** (or Llama2).
* **SQLite/PostgreSQL** (for storing chat history).

### **🛠️ Steps to Build**

1. **Install Dependencies**
   ```bash
   pip install fastapi openai uvicorn
   ```
2. **Set up OpenAI API Key** (`config.py`)
3. **Create Chat API Route** (`chat.py`)
   ```python
   import openai
   from fastapi import FastAPI

   app = FastAPI()

   @app.post("/chat/")
   async def chat(query: str):
       response = openai.ChatCompletion.create(
           model="gpt-4",
           messages=[{"role": "user", "content": query}]
       )
       return {"response": response.choices[0].message["content"]}
   ```
4. **Run API & Test with Swagger UI.**

---

## **3️⃣ FastAPI Web Scraper (BeautifulSoup + Celery)**

**🔹 Features:**

✅ Scrapes product data from e-commerce sites.

✅ Asynchronous scraping using Celery.

✅ Stores data in MongoDB.

✅ REST API to fetch scraped data.

### **📄 Tech Stack**

* **FastAPI** (API development).
* **Celery** (for async tasks).
* **BeautifulSoup** (for web scraping).
* **MongoDB** (for storing scraped data).

### **🛠️ Steps to Build**

1. **Install Dependencies**
   ```bash
   pip install fastapi celery beautifulsoup4 requests pymongo
   ```
2. **Create Scraper Function** (`scraper.py`)
   ```python
   from bs4 import BeautifulSoup
   import requests

   def scrape_website(url: str):
       response = requests.get(url)
       soup = BeautifulSoup(response.content, "html.parser")
       return {"title": soup.title.string}
   ```
3. **Integrate Scraper with FastAPI (`main.py`).**
4. **Store Data in MongoDB (`database.py`).**
5. **Use Celery for Background Tasks (`tasks.py`).**

---

## **4️⃣ URL Shortener API (FastAPI + Redis)**

**🔹 Features:**

✅ Converts long URLs into short URLs.

✅ Stores short URLs in Redis.

✅ Expiration feature for links.

✅ Fast redirection using FastAPI.

### **📄 Tech Stack**

* **FastAPI** (API development).
* **Redis** (key-value storage).
* **Pydantic** (validation).

### **🛠️ Steps to Build**

1. **Install Redis & FastAPI**
   ```bash
   pip install fastapi redis
   ```
2. **Create URL Shortener Logic** (`shortener.py`)
   ```python
   import redis
   from fastapi import FastAPI
   from pydantic import BaseModel
   import uuid

   app = FastAPI()
   redis_client = redis.Redis(host="localhost", port=6379, decode_responses=True)

   class URL(BaseModel):
       original_url: str

   @app.post("/shorten/")
   def shorten_url(url: URL):
       short_id = str(uuid.uuid4())[:6]
       redis_client.set(short_id, url.original_url, ex=86400)
       return {"short_url": f"http://localhost:8000/{short_id}"}

   @app.get("/{short_id}")
   def redirect(short_id: str):
       original_url = redis_client.get(short_id)
       if original_url:
           return {"redirect_to": original_url}
       return {"error": "URL not found"}
   ```
3. **Run FastAPI & Test in Swagger UI.**

---

## **5️⃣ Image Upload & Processing API**

**🔹 Features:**

✅ Upload images via FastAPI.

✅ Resize & apply filters using Pillow.

✅ Store images on local disk or cloud.

✅ Asynchronous processing with Celery.

### **📄 Tech Stack**

* **FastAPI** (API development).
* **Pillow** (image processing).
* **Celery** (background tasks).

### **🛠️ Steps to Build**

1. **Install Dependencies**
   ```bash
   pip install fastapi pillow aiofiles
   ```
2. **Create Image Upload Endpoint** (`image_api.py`)
   ```python
   from fastapi import FastAPI, File, UploadFile
   from PIL import Image
   import io

   app = FastAPI()

   @app.post("/upload/")
   async def upload_image(file: UploadFile = File(...)):
       image = Image.open(io.BytesIO(await file.read()))
       image = image.resize((300, 300))  # Resize image
       image.save(f"uploads/{file.filename}")
       return {"message": "Image uploaded and resized successfully!"}
   ```
3. **Test API with Swagger UI.**

---

## **Which Project Should You Build?**

| Project          | Complexity      | Best For                    |
| ---------------- | --------------- | --------------------------- |
| CRUD API         | 🟢 Beginner     | Learning FastAPI basics     |
| AI Chatbot       | 🟡 Intermediate | NLP & AI Integration        |
| Web Scraper      | 🟡 Intermediate | Asynchronous Processing     |
| URL Shortener    | 🟢 Beginner     | Redis & FastAPI Integration |
| Image Upload API | 🟡 Intermediate | File handling & Processing  |

---

## **🎯 Final Thoughts**

FastAPI is  **powerful** ,  **async-first** , and  **great for APIs** . Building hands-on projects will strengthen your **problem-solving skills** and  **make you job-ready** ! 🚀
