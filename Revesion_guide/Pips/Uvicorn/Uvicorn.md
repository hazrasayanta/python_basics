# **🚀 Uvicorn: High-Performance ASGI Server for FastAPI 🚀**

## **🔹 What is Uvicorn?**

Uvicorn is a **lightweight and high-performance** ASGI (Asynchronous Server Gateway Interface) server built on **uvloop** and  **httptools** . It is the recommended server for running FastAPI applications due to its **async-first** architecture.

---

## **🛠️ Installing Uvicorn**

You can install Uvicorn using pip:

```bash
pip install uvicorn
```

For better performance, install with `uvloop` and `httptools`:

```bash
pip install "uvicorn[standard]"
```

---

## **📄 Running a FastAPI App with Uvicorn**

### **Step 1: Create a FastAPI App**

📌 Create a file **`main.py`**

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def read_root():
    return {"message": "Hello, FastAPI with Uvicorn!"}
```

### **Step 2: Start the Server with Uvicorn**

Run the FastAPI app using Uvicorn:

```bash
uvicorn main:app --reload
```

📌 **Breakdown of the command:**

* `main` → Python file name (`main.py`).
* `app` → FastAPI instance (`app = FastAPI()`).
* `--reload` → Enables **auto-reloading** on code changes (useful for development).

---

## **⚡ Uvicorn Performance Boost with Workers**

For production, run Uvicorn with multiple workers:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
```

📌 **Parameters Explained:**

* `--host 0.0.0.0` → Exposes API to external users.
* `--port 8000` → Runs on port **8000** (default).
* `--workers 4` → Uses **4 worker processes** (for better performance).

---

## **🔄 Running Uvicorn with Gunicorn (Production-Ready)**

Gunicorn can manage multiple Uvicorn worker processes efficiently. Install Gunicorn:

```bash
pip install gunicorn
```

Run the server:

```bash
gunicorn -w 4 -k uvicorn.workers.UvicornWorker main:app
```

📌 **Why use Gunicorn?**

✅ Load balancing between multiple worker processes.

✅ Better resource management for production.

---

## **🔍 Uvicorn Logging & Debugging**

Enable detailed logging for debugging:

```bash
uvicorn main:app --log-level debug
```

📌 Log levels: `critical`, `error`, `warning`, `info`, `debug`.

---

## **🎯 When to Use Uvicorn?**

| Scenario                        | Use Uvicorn?                |
| ------------------------------- | --------------------------- |
| **Development**           | ✅ Yes (with `--reload`)  |
| **Production**            | ✅ Yes (with `--workers`) |
| **Behind Nginx/Gunicorn** | ✅ Yes (for scaling)        |
| **Synchronous APIs**      | ❌ No (Use Gunicorn)        |

---

## **🚀 Summary**

🔹 Uvicorn is a **fast, async-ready** server for  **FastAPI & ASGI apps** .

🔹 Use `--reload` for **development** and `--workers` for  **production** .

🔹 Combine Uvicorn with **Gunicorn** for large-scale deployment.
