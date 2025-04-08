## **Object-Oriented Programming (OOP) in Python – Interview Guide**

## Link : https://blog.algomaster.io/p/basic-oop-concepts-explained-with-code

### **What is OOP?**

Object-Oriented Programming (OOP) is a programming paradigm that uses **objects** and **classes** to structure and manage code efficiently. Python is an  **object-oriented language** , meaning everything in Python is an object.

### **Key OOP Concepts in Python**

1. **Class and Object**
2. **Encapsulation**
3. **Abstraction**
4. **Inheritance**
5. **Polymorphism**

---

## **1. Class and Object**

### **Class:** A blueprint for creating objects.

### **Object:** An instance of a class.

### **Example: Defining a Class and Creating an Object**

```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def display_info(self):
        return f"Car: {self.brand} {self.model}"

# Creating an object
my_car = Car("Tesla", "Model S")
print(my_car.display_info())  # Car: Tesla Model S
```

🔹 **`__init__`** is a constructor method that initializes object properties.

🔹 **Objects (`my_car`)** store unique data based on the class structure.

---

## **2. Encapsulation**

Encapsulation **hides the internal state** of an object and restricts direct access to it.

* Use **private variables** (`__var`) to enforce encapsulation.

### **Example: Encapsulation in Python**

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Private variable

    def deposit(self, amount):
        self.__balance += amount

    def get_balance(self):
        return self.__balance

# Creating an object
account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())  # 1500
```

🔹  **`__balance` is private** , meaning it **cannot** be accessed directly (`account.__balance`).

🔹 Access is allowed only through **getter** (`get_balance()`).

---

## **3. Abstraction**

Abstraction hides implementation details and exposes only  **necessary functionalities** .

* Use **abstract classes** (`ABC` module) to enforce abstraction.

### **Example: Abstraction in Python**

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def make_sound(self):
        pass  # Abstract method

class Dog(Animal):
    def make_sound(self):
        return "Woof!"

class Cat(Animal):
    def make_sound(self):
        return "Meow!"

dog = Dog()
print(dog.make_sound())  # Woof!
```

🔹 **Abstract classes (`ABC`)** prevent direct instantiation.

🔹 **Concrete subclasses (`Dog`, `Cat`)** must implement `make_sound()`.

---

## **4. Inheritance**

Inheritance allows a **child class** to derive properties from a  **parent class** .

* Supports **code reusability** and hierarchy.

### **Example: Inheritance in Python**

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "I make a sound"

class Dog(Animal):
    def speak(self):
        return "Woof!"

dog = Dog("Buddy")
print(dog.name)  # Buddy
print(dog.speak())  # Woof!
```

🔹 `Dog` **inherits** from `Animal`, reusing `name`.

🔹 `speak()` **is overridden** in the child class.

---

## **5. Polymorphism**

Polymorphism allows different objects to be treated **uniformly** while having  **different behaviors** .

### **Example: Method Overriding (Runtime Polymorphism)**

```python
class Bird:
    def fly(self):
        return "I can fly!"

class Penguin(Bird):
    def fly(self):
        return "I can't fly!"

birds = [Bird(), Penguin()]

for bird in birds:
    print(bird.fly())  # First: I can fly! | Second: I can't fly!
```

🔹 **Same method (`fly`) behaves differently** in `Bird` and `Penguin`.

---

## **OOP Interview Questions with Answers**

### **1. What is the difference between a class and an object?**

**Answer:**

* A **class** is a blueprint for creating objects.
* An **object** is an instance of a class with actual data.

---

### **2. What is encapsulation, and why is it important?**

**Answer:**

Encapsulation **restricts direct access** to an object’s data and allows controlled modifications.

* Protects data from accidental modification.
* Provides security via getter & setter methods.

---

### **3. How does inheritance help in OOP?**

**Answer:**

Inheritance enables **code reuse** by allowing a new class to inherit properties and methods from an existing class.

---

### **4. What is method overriding?**

**Answer:**

Method overriding allows a subclass to **provide a different implementation** of a method defined in its parent class.

---

### **5. What is the difference between method overloading and method overriding?**

| Feature         | Method Overloading                                           | Method Overriding                                 |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------- |
| Definition      | Multiple methods with the same name but different parameters | A subclass redefines a method from its superclass |
| When it happens | At**compile time**                                     | At**runtime**                               |
| Python Support  | Not directly supported                                       | Fully supported                                   |

🔹 Python **does not support method overloading** like Java/C++. Instead, we use  **default parameters** .

---

### **6. What is multiple inheritance, and how is it handled in Python?**

**Answer:**

Multiple inheritance allows a class to inherit from multiple classes.

**Example:**

```python
class A:
    def show(self):
        return "Class A"

class B:
    def show(self):
        return "Class B"

class C(A, B):  # Multiple inheritance
    pass

obj = C()
print(obj.show())  # Class A (Depends on MRO)
```

🔹 **Method Resolution Order (MRO)** decides which parent’s method to call first.

---

### **7. What is the `super()` function?**

**Answer:**

`super()` is used to call **methods of the parent class** inside a child class.

**Example:**

```python
class Parent:
    def show(self):
        return "Parent method"

class Child(Parent):
    def show(self):
        return super().show() + " + Child method"

obj = Child()
print(obj.show())  # Parent method + Child method
```

---

## **Summary of OOP Principles**

| Concept                  | Description                                         |
| ------------------------ | --------------------------------------------------- |
| **Class & Object** | Blueprint & instance of a class                     |
| **Encapsulation**  | Hides data using private variables                  |
| **Abstraction**    | Hides implementation details using abstract classes |
| **Inheritance**    | One class derives from another                      |
| **Polymorphism**   | Methods behave differently in different classes     |
