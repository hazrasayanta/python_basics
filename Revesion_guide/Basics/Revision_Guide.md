# **Python Revision Guide for Interviews

---

## **1. Core Python Concepts**

### **1.1 Data Types & Structures**

#### **Primitive Types**

| Data Type   | Example          | Description     |
| ----------- | ---------------- | --------------- |
| `int`     | `x = 10`       | Whole numbers   |
| `float`   | `y = 3.14`     | Decimal numbers |
| `str`     | `s = "Python"` | Text            |
| `bool`    | `flag = True`  | Boolean values  |
| `complex` | `z = 1 + 2j`   | Complex numbers |

```python
# Example of different data types
x = 10          # Integer
y = 3.14        # Float
s = "Python"    # String
flag = True     # Boolean
z = 1 + 2j      # Complex number

print(type(x), type(y), type(s), type(flag), type(z))
```

---

### **1.2 Mutable vs Immutable**

| Type      | Example          | Mutable? |
| --------- | ---------------- | -------- |
| `int`   | `x = 5`        | ❌ No    |
| `float` | `y = 3.14`     | ❌ No    |
| `str`   | `s = "hello"`  | ❌ No    |
| `tuple` | `t = (1,2,3)`  | ❌ No    |
| `list`  | `l = [1,2,3]`  | ✅ Yes   |
| `set`   | `s = {1,2,3}`  | ✅ Yes   |
| `dict`  | `d = {"a": 1}` | ✅ Yes   |

```python
# Immutable example (Strings)
s = "hello"
s[0] = "H"  # ❌ This will cause an error

# Mutable example (Lists)
l = [1, 2, 3]
l[0] = 100  # ✅ Allowed
```

---

## **2. String Manipulation**

### **2.1 String Methods**

```python
s = "  Python Programming  "
print(s.strip())  # Remove leading/trailing spaces
print(s.lower())  # Convert to lowercase
print(s.upper())  # Convert to uppercase
print(s.replace("Python", "Java"))  # Replace text
```

### **2.2 String Slicing**

```python
s = "Python"
print(s[0:3])  # 'Pyt' (start to index 3)
print(s[::-1])  # 'nohtyP' (Reverse string)
```

### **2.3 String Formatting**

```python
name = "John"
age = 25
print(f"My name is {name} and I am {age} years old.")  # f-string
```

---

## **3. Lists, Tuples, Sets, Dictionaries**

### **3.1 Lists (Mutable)**

```python
l = [10, 20, 30]
l.append(40)  # Add item
l.pop()       # Remove last item
print(l)
```

### **3.2 Tuples (Immutable)**

```python
t = (1, 2, 3)
print(t[0])  # Access element
```

### **3.3 Sets (Unique Items)**

```python
a = {1, 2, 3}
b = {3, 4, 5}
print(a.union(b))  # {1, 2, 3, 4, 5}
print(a.intersection(b))  # {3}
```

### **3.4 Dictionaries**

```python
d = {"name": "John", "age": 25}
print(d["name"])  # Access value
d["city"] = "New York"  # Add new key-value pair
```

---

## **4. Functions & Lambda Expressions**

### **4.1 Defining Functions**

```python
def add(a, b):
    return a + b

print(add(5, 10))
```

### **4.2 Lambda Functions**

```python
add = lambda a, b: a + b
print(add(5, 10))
```

### **4.3 Map, Filter, Reduce**

```python
nums = [1, 2, 3, 4, 5]

# Map (apply function to each element)
squares = list(map(lambda x: x**2, nums))
print(squares)  # [1, 4, 9, 16, 25]

# Filter (keep elements that satisfy condition)
evens = list(filter(lambda x: x % 2 == 0, nums))
print(evens)  # [2, 4]

# Reduce (cumulative sum)
from functools import reduce
total = reduce(lambda x, y: x + y, nums)
print(total)  # 15
```

---

## **5. Object-Oriented Programming (OOP)**

### **5.1 Classes & Objects**

```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def display(self):
        print(f"Car: {self.brand} {self.model}")

c1 = Car("Toyota", "Corolla")
c1.display()
```

### **5.2 Inheritance**

```python
class Animal:
    def sound(self):
        print("Animal makes a sound")

class Dog(Animal):
    def sound(self):
        print("Bark!")

d = Dog()
d.sound()  # Bark!
```

---

## **6. Exception Handling**

```python
try:
    x = 10 / 0  # ❌ Error
except ZeroDivisionError as e:
    print("Cannot divide by zero!")
finally:
    print("Execution completed.")
```

---

## **7. Multithreading & Multiprocessing**

### **7.1 Threading**

```python
import threading

def print_numbers():
    for i in range(5):
        print(i)

t = threading.Thread(target=print_numbers)
t.start()
t.join()
```

### **7.2 Multiprocessing**

```python
from multiprocessing import Process

def print_numbers():
    for i in range(5):
        print(i)

p = Process(target=print_numbers)
p.start()
p.join()
```

---

## **8. File Handling**

```python
# Writing to a file
with open("file.txt", "w") as f:
    f.write("Hello, Python!")

# Reading from a file
with open("file.txt", "r") as f:
    print(f.read())
```

---

## **9. Database Connection (MySQL)**

```python
import mysql.connector

conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="password",
    database="test_db"
)
cursor = conn.cursor()
cursor.execute("SELECT * FROM users")
for row in cursor.fetchall():
    print(row)
conn.close()
```

---

## **10. Web Scraping (BeautifulSoup)**

```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
response = requests.get(url)
soup = BeautifulSoup(response.text, "html.parser")
print(soup.title.text)
```

---

## **11. REST API with Flask**

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/api/data', methods=['GET'])
def get_data():
    return jsonify({"message": "Hello, World!"})

if __name__ == '__main__':
    app.run(debug=True)
```

---

## **12. Unit Testing**

```python
import unittest

def add(x, y):
    return x + y

class TestMath(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)

if __name__ == "__main__":
    unittest.main()
```

---

## **Final Tips**

✅ **Revise syntax & built-in functions**

✅ **Practice writing clean & efficient code**

✅ **Prepare for OOP, DB handling, and APIs**

✅ **Understand multithreading & multiprocessing**

✅ **Be ready to solve algorithmic problems**

Would you like me to add more specific topics or explanations?
