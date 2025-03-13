# **📄 Python-Docx: Working with Word Documents in Python**

`python-docx` is a Python library for  **creating, reading, and modifying Microsoft Word (`.docx`) documents** .

✅ **Why Use `python-docx`?**

* Automate **document generation** (e.g., reports, invoices)
* Extract **text & tables** from `.docx` files
* Modify **existing documents** (add text, images, styles)

---

## **1️⃣ Install python-docx**

```bash
pip install python-docx
```

---

## **2️⃣ Creating a New Word Document**

```python
from docx import Document

# Create a new document
doc = Document()

# Add a Title
doc.add_heading("My First Word Document", level=1)

# Add a Paragraph
doc.add_paragraph("This is an example paragraph in a Word document.")

# Save the document
doc.save("sample.docx")

print("Document saved successfully!")
```

✅ **What Happens?**

* A new Word document (`sample.docx`) is created.
* It contains a **heading** and a  **paragraph** .

---

## **3️⃣ Adding Formatted Text**

```python
p = doc.add_paragraph("This is a ")
p.add_run("bold").bold = True
p.add_run(" and ")
p.add_run("italic").italic = True
p.add_run(" word document.")

doc.save("formatted.docx")
```

✅ **What Happens?**

* Adds **bold** and *italic* text dynamically.

---

## **4️⃣ Working with Tables**

```python
# Add a Table (2 rows, 3 columns)
table = doc.add_table(rows=2, cols=3)

# Fill Table Data
table.cell(0, 0).text = "Name"
table.cell(0, 1).text = "Age"
table.cell(0, 2).text = "City"

table.cell(1, 0).text = "Alice"
table.cell(1, 1).text = "25"
table.cell(1, 2).text = "New York"

doc.save("table.docx")
```

✅ **What Happens?**

* A table with **headers and data** is created.

---

## **5️⃣ Reading an Existing Word Document**

```python
doc = Document("sample.docx")

# Extract text from all paragraphs
for para in doc.paragraphs:
    print(para.text)
```

✅ **Use Case:** Extract text from `.docx` files for  **processing or NLP tasks** .

---

## **6️⃣ Adding an Image**

```python
doc.add_picture("image.png", width=docx.shared.Inches(2))

doc.save("with_image.docx")
```

✅ **Why Resize?**

* To prevent **large images** from overflowing the document.

---

## **7️⃣ Setting Page Layout (Margins & Orientation)**

```python
from docx.shared import Inches
from docx.enum.section import WD_ORIENT

# Set Page Orientation
section = doc.sections[0]
section.orientation = WD_ORIENT.LANDSCAPE

# Set Margins
section.top_margin = Inches(1)
section.bottom_margin = Inches(1)
section.left_margin = Inches(1)
section.right_margin = Inches(1)

doc.save("formatted_page.docx")
```

✅ **Why Adjust Layout?**

* To create **professional** & **structured** documents.

---

## **🔹 Interview Questions on `python-docx`**

### **1️⃣ Basic Questions**

✔ What is `python-docx`, and why is it used?

✔ How do you create a new Word document in Python?

✔ How do you **add text and headings** to a `.docx` file?

### **2️⃣ Advanced Questions**

✔ How can you extract  **text from a Word document** ?

✔ How do you **format text dynamically** in a `.docx` file?

✔ How do you insert **tables and images** in Word using Python?

✔ Explain how you would **automate report generation** using `python-docx`.

---

## **🚀 Next Steps**

Would you like an **example with FastAPI + `python-docx`?** 🎯
