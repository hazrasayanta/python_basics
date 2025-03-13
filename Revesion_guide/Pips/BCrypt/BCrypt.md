# **🔐 BCrypt in Python: A Complete Guide**

## **🔹 What is BCrypt?**

`bcrypt` is a **password hashing function** designed for  **secure password storage** . It is widely used because of:

✅ **Salted Hashing** (Prevents rainbow table attacks)

✅ **Adaptive Work Factor** (Increases security over time)

✅ **Resistance to Brute-Force Attacks**

---

## **🔹 Installing `bcrypt`**

```bash
pip install bcrypt
```

---

## **1️⃣ Hashing a Password with BCrypt**

```python
import bcrypt

# Generate salt
salt = bcrypt.gensalt()

# Hash password
password = "my_secure_password".encode("utf-8")
hashed_password = bcrypt.hashpw(password, salt)

print(f"Hashed Password: {hashed_password}")
```

✅ **Why Use BCrypt?**

* Hashing is **one-way** (cannot be reversed)
* Salt **prevents precomputed attacks**

---

## **2️⃣ Verifying a Password**

```python
# User input for login
entered_password = "my_secure_password".encode("utf-8")

# Verify password
if bcrypt.checkpw(entered_password, hashed_password):
    print("✅ Password is correct!")
else:
    print("❌ Invalid password!")
```

✅ **Why Is This Secure?**

* **Ensures password correctness** without revealing the original hash
* **Mitigates brute-force attacks**

---

## **3️⃣ Adjusting Security with Work Factor**

BCrypt allows adjusting **computational cost** using the work factor (`rounds` parameter).

```python
# Increase rounds for stronger security
salt = bcrypt.gensalt(rounds=12)
hashed_password = bcrypt.hashpw(password, salt)
print(f"New Hashed Password: {hashed_password}")
```

✅ **Why Adjust Work Factor?**

* **Higher rounds = stronger security** but **slower performance**
* **Keeps passwords secure even as computing power increases**

---

## **🔹 Interview Questions on BCrypt**

### **1️⃣ Basic Questions**

✔ What is `bcrypt`, and why is it used?

✔ How does BCrypt protect against rainbow table attacks?

✔ What is the purpose of a salt in password hashing?

### **2️⃣ Advanced Questions**

✔ How does the work factor affect BCrypt security?

✔ Compare `bcrypt` vs. `pbkdf2` vs. `argon2`.

✔ Can you store and retrieve BCrypt hashes in a database?

---

## **🚀 Next Steps**

Would you like a **FastAPI authentication example using BCrypt?** 🎯
