# SOLID Principles in Python - Interview Guide

## 1. Introduction to SOLID Principles

SOLID is an acronym representing five design principles that help software developers create more maintainable, scalable, and robust code.

* **S** : Single Responsibility Principle (SRP)
* **O** : Open/Closed Principle (OCP)
* **L** : Liskov Substitution Principle (LSP)
* **I** : Interface Segregation Principle (ISP)
* **D** : Dependency Inversion Principle (DIP)

---

## 2. Explanation of Each Principle with Examples

### **1. Single Responsibility Principle (SRP)**

*"A class should have only one reason to change."*

**Example:**

```python
class Report:
    def __init__(self, data):
        self.data = data

    def generate_report(self):
        return f"Report Data: {self.data}"

    def save_to_file(self, filename):  # Violates SRP
        with open(filename, 'w') as file:
            file.write(self.generate_report())
```

✅ **Refactored:**

```python
class Report:
    def __init__(self, data):
        self.data = data

    def generate_report(self):
        return f"Report Data: {self.data}"

class FileManager:
    @staticmethod
    def save_to_file(filename, content):
        with open(filename, 'w') as file:
            file.write(content)
```

---

### **2. Open/Closed Principle (OCP)**

*"Software entities should be open for extension but closed for modification."*

**Example:**

```python
class Discount:
    def apply_discount(self, amount, discount_type):
        if discount_type == "fixed":
            return amount - 10
        elif discount_type == "percentage":
            return amount * 0.9
```

✅ **Refactored using polymorphism:**

```python
from abc import ABC, abstractmethod

class Discount(ABC):
    @abstractmethod
    def apply_discount(self, amount):
        pass

class FixedDiscount(Discount):
    def apply_discount(self, amount):
        return amount - 10

class PercentageDiscount(Discount):
    def apply_discount(self, amount):
        return amount * 0.9
```

---

### **3. Liskov Substitution Principle (LSP)**

*"Subtypes must be substitutable for their base types without altering correctness."*

**Example (Violation):**

```python
class Bird:
    def fly(self):
        return "I can fly"

class Penguin(Bird):
    def fly(self):  # Violates LSP
        raise Exception("Penguins cannot fly!")
```

✅ **Refactored:**

```python
class Bird:
    pass

class FlyingBird(Bird):
    def fly(self):
        return "I can fly"

class Penguin(Bird):
    def swim(self):
        return "I can swim"
```

---

### **4. Interface Segregation Principle (ISP)**

*"A class should not be forced to implement interfaces it does not use."*

**Example (Violation):**

```python
class Worker:
    def work(self):
        pass
  
    def eat(self):  # Not all workers need this
        pass
```

✅ **Refactored:**

```python
from abc import ABC, abstractmethod

class Workable(ABC):
    @abstractmethod
    def work(self):
        pass

class Eatable(ABC):
    @abstractmethod
    def eat(self):
        pass

class Employee(Workable, Eatable):
    def work(self):
        return "Working"
  
    def eat(self):
        return "Eating"

class Robot(Workable):
    def work(self):
        return "Working 24/7"
```

---

### **5. Dependency Inversion Principle (DIP)**

*"High-level modules should not depend on low-level modules. Both should depend on abstractions."*

**Example (Violation):**

```python
class MySQLDatabase:
    def connect(self):
        return "Connected to MySQL"

class Application:
    def __init__(self):
        self.db = MySQLDatabase()  # Direct dependency
```

✅ **Refactored using Dependency Injection:**

```python
class Database(ABC):
    @abstractmethod
    def connect(self):
        pass

class MySQLDatabase(Database):
    def connect(self):
        return "Connected to MySQL"

class Application:
    def __init__(self, db: Database):
        self.db = db
```

---

## 3. Most Asked Interview Questions on SOLID Principles

### **General Questions**

1. What are the SOLID principles, and why are they important?
2. How do SOLID principles improve code maintainability and scalability?

### **Principle-Specific Questions**

3. Can you explain the Single Responsibility Principle with an example?
4. How does the Open/Closed Principle help in software extensibility?
5. What is the Liskov Substitution Principle, and how would you implement it in Python?
6. Can you provide an example where Interface Segregation is beneficial?
7. How does the Dependency Inversion Principle promote decoupling in a system?

### **Scenario-Based Questions**

8. If you have a class handling user authentication and logging, which principle is violated, and how would you fix it?
9. How can you refactor a monolithic class into multiple classes following SOLID principles?
10. What would happen if we violate the Liskov Substitution Principle in an inheritance hierarchy?
