# **Python Revision Guide: FastAPI 🚀**

FastAPI is a high-performance web framework for building APIs with Python, leveraging type hints and async capabilities for speed and efficiency.

✅ **Install FastAPI and Uvicorn**

```bash
pip install fastapi uvicorn
```

---

## **1. Create a Simple FastAPI App**

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Welcome to FastAPI!"}
```

✅ **Run the app using Uvicorn:**

```bash
uvicorn main:app --reload
```

🚀 Visit **[http://127.0.0.1:8000](http://127.0.0.1:8000/)** to see the response.

---

## **2. Path and Query Parameters**

```python
@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "query": q}
```

✅ **Example Request:**

```bash
GET /items/42?q=hello
```

✅ **Response:**

```json
{"item_id": 42, "query": "hello"}
```

---

## **3. Request Body using Pydantic**

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float
    description: str = None

@app.post("/items/")
def create_item(item: Item):
    return {"message": "Item created!", "item": item}
```

✅ **Example Request (POST /items/):**

```json
{
    "name": "Laptop",
    "price": 1200.99,
    "description": "A gaming laptop"
}
```

✅ **Response:**

```json
{"message": "Item created!", "item": {"name": "Laptop", "price": 1200.99, "description": "A gaming laptop"}}
```

---

## **4. Handling Form Data & File Uploads**

```python
from fastapi import Form, File, UploadFile

@app.post("/login/")
def login(username: str = Form(...), password: str = Form(...)):
    return {"username": username}

@app.post("/upload/")
def upload_file(file: UploadFile = File(...)):
    return {"filename": file.filename}
```

---

## **5. Response Model (Data Validation & Filtering)**

```python
class ItemResponse(BaseModel):
    name: str
    price: float

@app.get("/items/{item_id}", response_model=ItemResponse)
def get_item(item_id: int):
    return {"name": "Phone", "price": 699.99, "stock": 50}  # 'stock' will be ignored
```

---

## **6. Dependency Injection**

```python
from typing import Optional

def common_params(q: Optional[str] = None, limit: int = 10):
    return {"query": q, "limit": limit}

@app.get("/products/")
def get_products(params: dict = Depends(common_params)):
    return params
```

---

## **7. Middleware for Logging**

```python
from fastapi.middleware.cors import CORSMiddleware
from fastapi.middleware.trustedhost import TrustedHostMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

@app.middleware("http")
async def log_requests(request, call_next):
    print(f"Request: {request.method} {request.url}")
    response = await call_next(request)
    return response
```

---

## **8. JWT Authentication**

```python
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.get("/users/me")
async def read_users_me(token: str = Depends(oauth2_scheme)):
    return {"token": token}
```

---

## **9. Background Tasks**

```python
from fastapi import BackgroundTasks

def write_log(message: str):
    with open("log.txt", "a") as f:
        f.write(message + "\n")

@app.post("/log/")
def log_message(message: str, background_tasks: BackgroundTasks):
    background_tasks.add_task(write_log, message)
    return {"message": "Log scheduled"}
```

---

## **10. Connecting to a Database (SQLAlchemy + MySQL)**

```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "mysql+pymysql://user:password@localhost/mydatabase"

engine = create_engine(DATABASE_URL)
SessionLocal = sessionmaker(bind=engine)
Base = declarative_base()

class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True, index=True)
    name = Column(String)

Base.metadata.create_all(bind=engine)

@app.get("/users/")
def get_users():
    db = SessionLocal()
    users = db.query(User).all()
    db.close()
    return users
```

---

## **11. Running FastAPI with Gunicorn for Production**

Create a `gunicorn_config.py` file:

```python
workers = 4
bind = "0.0.0.0:8000"
```

✅ **Run with Gunicorn & Uvicorn:**

```bash
gunicorn -k uvicorn.workers.UvicornWorker main:app
```

---

## **🚀 Summary**

✅ **FastAPI is an async framework for building APIs.**

✅ **Use `Pydantic` for request validation.**

✅ **Middleware, JWT, and Dependency Injection improve scalability.**

✅ **SQLAlchemy is used for database integration.**

✅ **Use `Uvicorn` or `Gunicorn` for production deployment.**
