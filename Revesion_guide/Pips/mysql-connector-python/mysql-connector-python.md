# **🔹 MySQL Connector for Python (`mysql-connector-python`)**

## **🔹 What is `mysql-connector-python`?**

`mysql-connector-python` is an official MySQL driver for Python that allows interaction with **MySQL databases** without additional dependencies like SQLAlchemy.

✅ **Key Features:**

* **Pure Python implementation** (no external libraries needed)
* **Supports connection pooling**
* **Provides both cursor and dictionary-based results**
* **Supports prepared statements for security**

---

## **🔹 Installing MySQL Connector**

```bash
pip install mysql-connector-python
```

---

## **1️⃣ Connecting to MySQL Database**

```python
import mysql.connector

# Create a connection
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="yourpassword",
    database="testdb"
)

if conn.is_connected():
    print("Connected to MySQL Database!")

conn.close()  # Close connection
```

✅ **Why Use `.is_connected()`?**

* Ensures the connection is **successfully established**

---

## **2️⃣ Creating a Table**

```python
conn = mysql.connector.connect(host="localhost", user="root", password="yourpassword", database="testdb")
cursor = conn.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE
)
""")

print("Table created successfully!")
conn.close()
```

✅ **Why Use `IF NOT EXISTS`?**

* **Prevents errors** if the table already exists

---

## **3️⃣ Inserting Data**

```python
conn = mysql.connector.connect(host="localhost", user="root", password="yourpassword", database="testdb")
cursor = conn.cursor()

query = "INSERT INTO users (name, email) VALUES (%s, %s)"
values = ("John Doe", "john@example.com")

cursor.execute(query, values)
conn.commit()  # Commit transaction

print(f"{cursor.rowcount} record inserted.")
conn.close()
```

✅ **Why Use `commit()`?**

* Ensures **data is saved** permanently

---

## **4️⃣ Fetching Data**

### **(a) Fetch One Record**

```python
cursor.execute("SELECT * FROM users WHERE name = %s", ("John Doe",))
user = cursor.fetchone()
print(user)  # Output: (1, 'John Doe', 'john@example.com')
```

### **(b) Fetch All Records**

```python
cursor.execute("SELECT * FROM users")
users = cursor.fetchall()

for user in users:
    print(user)
```

✅ **Why Use Parameterized Queries (`%s`)?**

* **Prevents SQL injection attacks**

---

## **5️⃣ Updating & Deleting Data**

### **(a) Updating a User**

```python
query = "UPDATE users SET email = %s WHERE name = %s"
values = ("newemail@example.com", "John Doe")

cursor.execute(query, values)
conn.commit()
print(f"{cursor.rowcount} record updated.")
```

### **(b) Deleting a User**

```python
query = "DELETE FROM users WHERE name = %s"
values = ("John Doe",)

cursor.execute(query, values)
conn.commit()
print(f"{cursor.rowcount} record deleted.")
```

✅ **Why Use `rowcount`?**

* Shows how many rows were **affected by the query**

---

## **6️⃣ Using Dictionary Cursor**

```python
cursor = conn.cursor(dictionary=True)  # Enables column-name keys
cursor.execute("SELECT * FROM users")

for user in cursor.fetchall():
    print(user["name"], "-", user["email"])
```

✅ **Why Use `dictionary=True`?**

* Access data **as a dictionary** instead of a tuple

---

## **7️⃣ Connection Pooling (Performance Optimization)**

```python
from mysql.connector import pooling

db_pool = pooling.MySQLConnectionPool(
    pool_name="mypool",
    pool_size=5,
    host="localhost",
    user="root",
    password="yourpassword",
    database="testdb"
)

conn = db_pool.get_connection()  # Get a connection from the pool
cursor = conn.cursor()
cursor.execute("SELECT COUNT(*) FROM users")
print(cursor.fetchone())
conn.close()
```

✅ **Why Use Connection Pooling?**

* **Reuses connections** , reducing overhead in high-load applications

---

## **🔹 Interview Questions on `mysql-connector-python`**

### **1️⃣ Basic Questions**

✔ What is `mysql-connector-python`?

✔ How do you connect Python to MySQL?

✔ What is the purpose of `.commit()` in transactions?

### **2️⃣ Advanced Questions**

✔ How do you prevent **SQL injection** in MySQL queries?

✔ What is a  **connection pool** , and why is it used?

✔ How does **dictionary cursor** differ from a normal cursor?

✔ How can you execute **multiple queries efficiently** in `mysql-connector-python`?

---

## **🚀 Next Steps**

Would you like an **example with FastAPI + MySQL?** 🎯
