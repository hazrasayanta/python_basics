# **🔹 SQLAlchemy: A Complete Guide**

## **🔹 What is SQLAlchemy?**

`SQLAlchemy` is a powerful **ORM (Object Relational Mapper)** and **SQL toolkit** for Python.

It allows developers to interact with databases using  **Python objects instead of raw SQL queries** .

✅ **Key Features:**

* **ORM & Core API** for flexibility
* **Support for multiple databases** (MySQL, PostgreSQL, SQLite, etc.)
* **Efficient query execution & connection pooling**
* **Declarative syntax for defining models**

---

## **🔹 Installing SQLAlchemy**

```bash
pip install sqlalchemy
```

For  **MySQL** :

```bash
pip install pymysql
```

For  **PostgreSQL** :

```bash
pip install psycopg2
```

---

## **1️⃣ Connecting to a Database**

```python
from sqlalchemy import create_engine

# Replace with your DB URL
DATABASE_URL = "sqlite:///test.db"  # For SQLite
engine = create_engine(DATABASE_URL, echo=True)

print("Database connected successfully!")
```

✅ **Why Use `create_engine`?**

* Establishes a **database connection**
* Supports **thread pooling & transactions**

---

## **2️⃣ Defining a Model (ORM)**

```python
from sqlalchemy.orm import declarative_base
from sqlalchemy import Column, Integer, String

Base = declarative_base()

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True, autoincrement=True)
    name = Column(String(50))
    email = Column(String(100), unique=True)

print("User model defined!")
```

✅ **Why Use ORM?**

* Maps **Python classes to database tables**
* Enables **object-oriented database interactions**

---

## **3️⃣ Creating the Table**

```python
Base.metadata.create_all(engine)
print("Tables created successfully!")
```

✅ **Why Use `create_all()`?**

* Ensures **database schema is created** automatically

---

## **4️⃣ Inserting Data**

```python
from sqlalchemy.orm import sessionmaker

Session = sessionmaker(bind=engine)
session = Session()

new_user = User(name="John Doe", email="john@example.com")
session.add(new_user)
session.commit()

print("New user added successfully!")
```

✅ **Why Use Sessions?**

* Manages **transactions automatically**
* Ensures **data integrity**

---

## **5️⃣ Querying Data**

```python
user = session.query(User).filter_by(name="John Doe").first()
print(f"User Found: {user.name} - {user.email}")
```

✅ **Why Use Query API?**

* Allows **complex filtering & retrieval**
* **Optimized SQL queries** under the hood

---

## **6️⃣ Updating & Deleting Data**

```python
# Updating a user
user.email = "newemail@example.com"
session.commit()
print("User updated successfully!")

# Deleting a user
session.delete(user)
session.commit()
print("User deleted successfully!")
```

✅ **Why Use ORM?**

* **Safe and controlled** database operations

---

## **🔹 Interview Questions on SQLAlchemy**

### **1️⃣ Basic Questions**

✔ What is SQLAlchemy?

✔ What are the benefits of using ORM over raw SQL?

✔ How do you define a model in SQLAlchemy?

### **2️⃣ Advanced Questions**

✔ Explain the difference between  **SQLAlchemy Core vs ORM** .

✔ How does **session management** work in SQLAlchemy?

✔ How does **lazy loading** work in relationships?

✔ What is the purpose of  **declarative base** ?

---

## **🚀 Next Steps**

Would you like a **FastAPI + SQLAlchemy integration example?** 🎯
