# 🔐 **Passlib: Secure Password Hashing in Python**

## **📌 What is Passlib?**

Passlib is a **password hashing library** in Python that provides **secure and easy-to-use** password hashing methods. It supports multiple algorithms, including:

✅ **bcrypt** (Recommended)

✅ **PBKDF2**

✅ **argon2** (Highly secure)

✅ **SHA512-Crypt**

---

## **🛠️ Installation**

Install Passlib with bcrypt support:

```bash
pip install passlib[bcrypt]
```

---

## **🔑 Hashing Passwords with Passlib**

### **1️⃣ Hash a Password Using bcrypt**

```python
from passlib.hash import bcrypt

password = "MySecurePassword123"

# Hash the password
hashed_password = bcrypt.hash(password)
print("Hashed Password:", hashed_password)
```

📌 **bcrypt automatically generates a unique salt** for each hash.

---

### **2️⃣ Verify a Password**

```python
# Verify password input
if bcrypt.verify("MySecurePassword123", hashed_password):
    print("✅ Password is correct!")
else:
    print("❌ Incorrect password!")
```

📌 **`verify()` checks if a given password matches the stored hash.**

---

## **⚡ Using Passlib with PBKDF2 (More Secure)**

```python
from passlib.hash import pbkdf2_sha256

# Hash password with PBKDF2-SHA256
hashed_pw = pbkdf2_sha256.hash("MySecurePassword")
print("PBKDF2 Hash:", hashed_pw)

# Verify password
if pbkdf2_sha256.verify("MySecurePassword", hashed_pw):
    print("✅ Password Matched!")
```

📌 PBKDF2 applies **multiple iterations** to increase security.

---

## **🔹 Storing Hashed Passwords in a Database**

1️⃣ Store `hashed_password` in the database.

2️⃣ When a user logs in, retrieve the hash and use `verify()` to check.

```python
# Simulating database storage
user_db = {
    "username": "john_doe",
    "password_hash": bcrypt.hash("SuperSecret123")
}

# Simulating login
user_input = "SuperSecret123"

if bcrypt.verify(user_input, user_db["password_hash"]):
    print("✅ Login Successful!")
else:
    print("❌ Incorrect Password!")
```

---

## **⚠️ Security Best Practices**

✅ **Never store raw passwords** in a database.

✅ **Use bcrypt, PBKDF2, or Argon2** (avoid SHA-1, MD5).

✅ **Use a unique salt** for each password.

✅ **Use a high number of iterations** for PBKDF2.

---

## **🔥 Common Interview Questions on Passlib**

### **1️⃣ Why should you use Passlib instead of manually hashing passwords?**

✅ Passlib **automates salting & hashing** securely.

✅ It supports  **modern password hashing algorithms** .

✅ Protects against  **rainbow table attacks** .

### **2️⃣ What is the best password hashing algorithm?**

| Algorithm               | Security Level | Performance | Notes                                           |
| ----------------------- | -------------- | ----------- | ----------------------------------------------- |
| **bcrypt**        | High           | Medium      | **Recommended for most applications**     |
| **PBKDF2-SHA256** | High           | Slower      | Used by**Django & OpenSSL**               |
| **Argon2**        | Very High      | Slower      | **Best security, used in modern systems** |

### **3️⃣ How does bcrypt protect against brute force attacks?**

✅ **Key stretching** (slower hashing process).

✅ **Adaptive hashing** (increases complexity over time).

✅ **Salt generation** (prevents identical hashes for same passwords).

---

## **🚀 Summary**

✔ Passlib provides  **secure password hashing & verification** .

✔ Supports  **bcrypt, PBKDF2, Argon2, and more** .

✔ **Best practice:** Use  **bcrypt or Argon2** , store only hashes, and always verify with `verify()`.
