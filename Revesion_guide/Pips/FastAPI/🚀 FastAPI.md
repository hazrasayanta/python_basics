# 🚀 **FastAPI Interview Guide** 🚀

FastAPI is a modern, high-performance web framework for building APIs with Python. It is built on **Starlette** (for web handling) and **Pydantic** (for data validation).

This guide covers  **core concepts** ,  **code snippets** ,  **diagrams** , and  **common interview questions** .

---

## **1️⃣ Why FastAPI? (Key Features)**

### ✅ **High Performance** - Asynchronous support (built on Starlette & Pydantic).

### ✅ **Automatic Documentation** - Swagger UI & ReDoc.

### ✅ **Type Hints** - Uses Python **type hints** for validation.

### ✅ **Dependency Injection** - Built-in support for managing dependencies.

### ✅ **Data Serialization** - Uses **Pydantic** for request/response models.

---

## **2️⃣ FastAPI Architecture Diagram**

```
Client → FastAPI Router → Business Logic → Response Model → Return JSON Response
```

🔹 **Diagram Representation**

```plaintext
 ┌────────────┐      ┌──────────────┐      ┌──────────────┐      ┌────────────┐
 │   Client   │ ───► │   FastAPI    │ ───► │  Business    │ ───► │  Response  │
 │ (Frontend) │      │  (Router)    │      │  Logic       │      │  (JSON)    │
 └────────────┘      └──────────────┘      └──────────────┘      └────────────┘
```

---

## **3️⃣ Setting Up FastAPI**

### **📌 Install FastAPI & Uvicorn**

```bash
pip install fastapi uvicorn
```

### **📄 `main.py` - Basic API**

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"message": "Hello, FastAPI!"}
```

### **Run the Server**

```bash
uvicorn main:app --reload
```

🟢 Open **Swagger UI** at:

📌 `http://127.0.0.1:8000/docs`

🟢 Open **ReDoc** at:

📌 `http://127.0.0.1:8000/redoc`

---

## **4️⃣ Path & Query Parameters**

### **📄 Example: Path & Query Parameters**

```python
@app.get("/items/{item_id}")
def read_item(item_id: int, category: str = "default"):
    return {"item_id": item_id, "category": category}
```

### 🔹 **Usage:**

```
GET /items/42?category=electronics
```

🔹 **Response:**

```json
{"item_id": 42, "category": "electronics"}
```

---

## **5️⃣ Request & Response Models**

🔹 **Uses Pydantic for Validation**

### **📄 `models.py`**

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float
    in_stock: bool = True
```

### **📄 `main.py` - Request Body Handling**

```python
@app.post("/items/")
def create_item(item: Item):
    return {"message": "Item created", "item": item}
```

🔹 **Example Request:**

```json
{
  "name": "Laptop",
  "price": 999.99
}
```

🔹 **Example Response:**

```json
{
  "message": "Item created",
  "item": {
    "name": "Laptop",
    "price": 999.99,
    "in_stock": true
  }
}
```

---

## **6️⃣ Dependency Injection**

🔹 **Useful for Database Connections & Authentication**

### **📄 Example: Dependency Injection**

```python
from fastapi import Depends

def get_db():
    return {"db": "Connected"}

@app.get("/db")
def read_db(db=Depends(get_db)):
    return db
```

---

## **7️⃣ Middleware**

🔹 **Logging requests before processing them.**

### **📄 Example: Middleware**

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["*"],
    allow_headers=["*"]
)
```

---

## **8️⃣ Authentication with OAuth2**

🔹 **JWT Authentication Example**

### **📄 Install Dependencies**

```bash
pip install python-jose[cryptography] passlib[bcrypt]
```

### **📄 Authentication Example**

```python
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.get("/users/me")
def read_users_me(token: str = Depends(oauth2_scheme)):
    return {"token": token}
```

---

## **9️⃣ Database Connection (SQLAlchemy)**

🔹 **FastAPI supports SQLAlchemy for relational databases**

### **📄 Install Dependencies**

```bash
pip install sqlalchemy databases psycopg2
```

### **📄 Database Setup**

```python
from sqlalchemy import create_engine

DATABASE_URL = "postgresql://user:password@localhost/dbname"
engine = create_engine(DATABASE_URL)
```

---

## **🔟 FastAPI Interview Questions**

### **📝 Basic Questions**

1. **What is FastAPI and why is it popular?**
2. **How does FastAPI compare with Flask and Django?**
3. **How does FastAPI handle automatic documentation?**
4. **What is Pydantic and why is it used in FastAPI?**
5. **Explain the difference between query parameters and path parameters in FastAPI.**

### **📝 Advanced Questions**

6. **How does FastAPI handle async operations?**
7. **Explain Dependency Injection in FastAPI.**
8. **What is the purpose of middleware in FastAPI?**
9. **How do you secure a FastAPI application?**
10. **How does FastAPI handle WebSockets?**
