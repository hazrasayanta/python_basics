# **🔐 Python-JOSE: JWT Authentication in Python**

## **📌 What is python-jose?**

Python-JOSE (`pyjwt[jose]`) is a **lightweight library** for handling **JSON Web Tokens (JWTs)** using **JOSE (JavaScript Object Signing and Encryption)** standards. It supports:

✅ **JWT (JSON Web Tokens)**

✅ **JWS (JSON Web Signature)**

✅ **JWE (JSON Web Encryption)**

---

## **🛠️ Installation**

Install Python-JOSE with dependencies:

```bash
pip install python-jose[cryptography]
```

---

## **🔑 Generating & Verifying JWTs**

### **1️⃣ Generate a JWT Token**

```python
from jose import jwt
import datetime

# Secret Key (Use Environment Variable in Production)
SECRET_KEY = "mysecret"

# Payload (Data inside JWT)
payload = {
    "user_id": 123,
    "exp": datetime.datetime.utcnow() + datetime.timedelta(hours=1)  # Expiration time
}

# Generate JWT Token
token = jwt.encode(payload, SECRET_KEY, algorithm="HS256")
print("Generated Token:", token)
```

---

### **2️⃣ Decode & Verify JWT Token**

```python
# Decode JWT Token
try:
    decoded_payload = jwt.decode(token, SECRET_KEY, algorithms=["HS256"])
    print("Decoded Payload:", decoded_payload)
except jwt.ExpiredSignatureError:
    print("Token has expired!")
except jwt.JWTError:
    print("Invalid token!")
```

📌 **Key Points:**

* **`jwt.encode()`** → Generates a token.
* **`jwt.decode()`** → Validates and decodes the token.
* **Exception Handling** for **expired/invalid** tokens.

---

## **🔄 Using Public & Private Keys (RS256 Algorithm)**

Python-JOSE also supports **asymmetric encryption (RSA, EC)** for JWTs.

### **🔹 Generate JWT using an RSA Private Key**

```python
from jose import jwt

# Load RSA Private Key
with open("private.pem", "r") as f:
    private_key = f.read()

# Generate JWT
token = jwt.encode({"user_id": 123}, private_key, algorithm="RS256")
print("JWT with RS256:", token)
```

### **🔹 Verify JWT using RSA Public Key**

```python
# Load RSA Public Key
with open("public.pem", "r") as f:
    public_key = f.read()

# Verify Token
decoded = jwt.decode(token, public_key, algorithms=["RS256"])
print("Decoded Payload:", decoded)
```

📌 **RSA is more secure** since it uses separate public/private keys.

---

## **🔥 Common Interview Questions on python-jose**

### **1️⃣ What is python-jose and how does it handle JWTs?**

**Answer:** Python-JOSE is a library for creating, encoding, decoding, and verifying JWTs using JOSE standards. It supports multiple encryption and signing algorithms like  **HS256, RS256, ES256** .

### **2️⃣ What is the difference between HS256 and RS256?**

| Algorithm | Type       | Uses Secret Key?              | Security Level |
| --------- | ---------- | ----------------------------- | -------------- |
| HS256     | Symmetric  | Yes (shared key)              | Medium         |
| RS256     | Asymmetric | No (uses Public/Private keys) | High           |

* **HS256** → Faster but uses the same key for signing & verifying (shared secret).
* **RS256** → More secure as it uses a **private key** for signing and a **public key** for verification.

### **3️⃣ What are some security best practices when using JWTs?**

✅ **Use RS256 instead of HS256** for better security.

✅ **Set expiration (`exp`)** to prevent replay attacks.

✅ **Store JWTs securely** (avoid local storage in frontend apps).

✅ **Rotate keys regularly** to prevent misuse.

### **4️⃣ How do you handle expired JWTs?**

Use exception handling:

```python
try:
    jwt.decode(token, SECRET_KEY, algorithms=["HS256"])
except jwt.ExpiredSignatureError:
    print("Token expired, request a new one!")
```

**Solution:** Implement **refresh tokens** to get a new JWT.

---

## **🚀 Summary**

✔ Python-JOSE simplifies  **JWT creation, verification, and encryption** .

✔ Supports  **HS256 (HMAC) and RS256 (RSA key pair)** .

✔ **Security Best Practices:** Use  **RS256, set expiration, store securely** .
