# **📄 PyPDF: Working with PDFs in Python**

`PyPDF` (formerly `PyPDF2`) is a powerful **pure Python** library for  **reading, writing, and manipulating PDFs** .

---

## **1️⃣ Install PyPDF**

```bash
pip install pypdf
```

---

## **2️⃣ Extracting Text from a PDF**

```python
from pypdf import PdfReader

# Load PDF file
reader = PdfReader("sample.pdf")

# Extract text from all pages
for page in reader.pages:
    print(page.extract_text())
```

✅ **Use Case:** Extract text for  **NLP, search indexing, and text analysis** .

---

## **3️⃣ Extracting Metadata from a PDF**

```python
print(reader.metadata)
```

✅ **What Can You Get?**

* Title, Author, Subject, Producer, Creation Date, etc.

---

## **4️⃣ Merging Multiple PDFs**

```python
from pypdf import PdfMerger

merger = PdfMerger()
merger.append("file1.pdf")
merger.append("file2.pdf")
merger.write("merged.pdf")
merger.close()
```

✅ **Use Case:** Automate  **merging invoices, reports, or multi-part documents** .

---

## **5️⃣ Splitting a PDF (Extract Specific Pages)**

```python
from pypdf import PdfWriter

reader = PdfReader("sample.pdf")
writer = PdfWriter()

# Extract pages 1 to 3
for i in range(3):  
    writer.add_page(reader.pages[i])

writer.write("split.pdf")
writer.close()
```

✅ **Use Case:** Extract specific **sections** from large PDFs.

---

## **6️⃣ Rotating Pages**

```python
writer = PdfWriter()
for page in reader.pages:
    page.rotate(90)  # Rotate 90 degrees
    writer.add_page(page)

writer.write("rotated.pdf")
writer.close()
```

✅ **Use Case:** Fix  **scanned or misaligned documents** .

---

## **7️⃣ Adding a Watermark**

```python
watermark = PdfReader("watermark.pdf").pages[0]
writer = PdfWriter()

for page in reader.pages:
    page.merge_page(watermark)
    writer.add_page(page)

writer.write("watermarked.pdf")
writer.close()
```

✅ **Use Case:** Add **branding or security marks** to PDFs.

---

## **8️⃣ Encrypting a PDF (Password Protection)**

```python
writer = PdfWriter()

for page in reader.pages:
    writer.add_page(page)

writer.encrypt("mypassword")  # Set password
writer.write("secured.pdf")
writer.close()
```

✅ **Use Case:** Secure  **confidential documents** .

---

## **🔹 Interview Questions on `PyPDF`**

### **1️⃣ Basic Questions**

✔ What is `pypdf`, and why is it used?

✔ How do you **extract text** from a PDF using Python?

✔ How can you  **merge multiple PDFs** ?

### **2️⃣ Advanced Questions**

✔ How do you  **extract images from a PDF** ?

✔ How can you  **password-protect a PDF** ?

✔ How do you **add a watermark** to a PDF using `pypdf`?

✔ How do you extract only **specific pages** from a large PDF?

---

## **🚀 Next Steps**

Would you like a **FastAPI + PyPDF API for PDF processing?** 🎯
