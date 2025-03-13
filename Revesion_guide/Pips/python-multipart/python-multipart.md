# **📌 `python-multipart` in FastAPI – Handling File Uploads & Forms**

`python-multipart` is used in **FastAPI** to handle  **form data and file uploads** . It parses `multipart/form-data` requests, which are required for uploading files and submitting HTML forms.

---

## **📌 Installation**

Install `python-multipart` before handling form data in FastAPI:

```bash
pip install python-multipart
```

---

## **🛠️ 1. Handling Form Data**

To accept  **form fields** , use `Form` from `fastapi`.

```python
from fastapi import FastAPI, Form

app = FastAPI()

@app.post("/submit-form/")
async def submit_form(username: str = Form(...), email: str = Form(...)):
    return {"username": username, "email": email}
```

### **📌 Testing via cURL**

```bash
curl -X POST "http://127.0.0.1:8000/submit-form/" -d "username=JohnDoe&email=john@example.com"
```

✅ **Response:**

```json
{"username": "JohnDoe", "email": "john@example.com"}
```

---

## **🛠️ 2. Handling File Uploads**

Use `UploadFile` and `File` to accept  **uploaded files** .

```python
from fastapi import FastAPI, File, UploadFile

app = FastAPI()

@app.post("/upload/")
async def upload_file(file: UploadFile = File(...)):
    return {"filename": file.filename, "content_type": file.content_type}
```

### **📌 Testing via cURL**

```bash
curl -X POST "http://127.0.0.1:8000/upload/" -F "file=@test.txt"
```

✅ **Response:**

```json
{"filename": "test.txt", "content_type": "text/plain"}
```

---

## **🛠️ 3. Saving Uploaded Files**

To **save** an uploaded file:

```python
@app.post("/upload-save/")
async def upload_save(file: UploadFile = File(...)):
    with open(f"uploads/{file.filename}", "wb") as buffer:
        buffer.write(await file.read())
    return {"message": f"File '{file.filename}' saved!"}
```

📌 **Ensure the `uploads/` folder exists before running this!**

---

## **🛠️ 4. Uploading Multiple Files**

FastAPI allows **multiple file uploads** easily.

```python
@app.post("/upload-multiple/")
async def upload_multiple(files: list[UploadFile] = File(...)):
    return {"filenames": [file.filename for file in files]}
```

### **📌 Testing via cURL**

```bash
curl -X POST "http://127.0.0.1:8000/upload-multiple/" -F "files=@test1.txt" -F "files=@test2.txt"
```

✅ **Response:**

```json
{"filenames": ["test1.txt", "test2.txt"]}
```

---

## **🔹 Key Takeaways**

✔ `python-multipart` **parses form data & file uploads** in FastAPI.

✔ `Form(...)` is used to  **receive form fields** .

✔ `File(...)` and `UploadFile` handle  **file uploads** .

✔ Multiple files can be  **uploaded at once** .
