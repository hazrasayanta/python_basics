
## **SOLID Principles in Python – Interview Guide**

### **1. What are the SOLID principles, and why are they important?**

**Answer:**

SOLID is an acronym representing five principles of object-oriented design that help in creating maintainable, scalable, and flexible software. These principles are:

* **S**ingle Responsibility Principle (SRP)
* **O**pen/Closed Principle (OCP)
* **L**iskov Substitution Principle (LSP)
* **I**nterface Segregation Principle (ISP)
* **D**ependency Inversion Principle (DIP)

**Importance:**

* Helps in reducing code complexity.
* Improves code maintainability and extensibility.
* Makes debugging and testing easier.
* Enhances reusability and separation of concerns.

---

### **2. How do SOLID principles improve code maintainability and scalability?**

**Answer:**

SOLID principles improve code maintainability and scalability by:

* **Reducing dependencies** , making it easier to change one part of the system without affecting others.
* **Encouraging modular design** , making it easy to extend functionality.
* **Enhancing readability** , making code more understandable for new developers.
* **Supporting testability** , making unit testing more effective.

---

### **3. Can you explain the Single Responsibility Principle with an example?**

**Answer:**

**Single Responsibility Principle (SRP):** A class should have only one reason to change, meaning it should have only  **one job** .

**Example (Violating SRP):**

```python
class Report:
    def generate_report(self):
        return "Report Data"
  
    def save_to_file(self, filename):
        with open(filename, 'w') as f:
            f.write(self.generate_report())
```

Here, `Report` handles both **report generation** and  **file saving** , violating SRP.

**Refactored Code (Following SRP):**

```python
class Report:
    def generate_report(self):
        return "Report Data"

class FileSaver:
    def save_to_file(self, filename, content):
        with open(filename, 'w') as f:
            f.write(content)

report = Report()
saver = FileSaver()
saver.save_to_file("report.txt", report.generate_report())
```

Now, each class has a single responsibility.

---

### **4. How does the Open/Closed Principle help in software extensibility?**

**Answer:**

**Open/Closed Principle (OCP):** A class should be  **open for extension but closed for modification** . This means we should  **add new functionality without altering existing code** .

**Example (Violating OCP):**

```python
class Discount:
    def get_discount(self, customer_type):
        if customer_type == "regular":
            return 10
        elif customer_type == "vip":
            return 20
```

Adding a new customer type requires modifying this method, violating OCP.

**Refactored Code (Following OCP using Polymorphism):**

```python
from abc import ABC, abstractmethod

class Discount(ABC):
    @abstractmethod
    def get_discount(self):
        pass

class RegularDiscount(Discount):
    def get_discount(self):
        return 10

class VIPDiscount(Discount):
    def get_discount(self):
        return 20

def calculate_discount(discount: Discount):
    return discount.get_discount()

print(calculate_discount(RegularDiscount()))  # 10
print(calculate_discount(VIPDiscount()))  # 20
```

Now, we can extend the system by adding new discount types without modifying existing code.

---

### **5. What is the Liskov Substitution Principle, and how would you implement it in Python?**

**Answer:**

**Liskov Substitution Principle (LSP):** Subtypes must be substitutable for their base types without altering the correctness of the program.

**Example (Violating LSP):**

```python
class Bird:
    def fly(self):
        return "Flying"

class Penguin(Bird):
    def fly(self):
        raise Exception("Penguins cannot fly!")
```

Here, `Penguin` inherits `Bird`, but it cannot fly, violating LSP.

**Refactored Code (Following LSP using Interfaces):**

```python
class Bird:
    pass

class FlyingBird(Bird):
    def fly(self):
        return "Flying"

class Penguin(Bird):
    def swim(self):
        return "Swimming"

sparrow = FlyingBird()
penguin = Penguin()
print(sparrow.fly())  # Works fine
print(penguin.swim())  # Works fine without violating LSP
```

Now, `Penguin` does not inherit the `fly()` method it cannot support.

---

### **6. Can you provide an example where Interface Segregation is beneficial?**

**Answer:**

**Interface Segregation Principle (ISP):** Clients should not be forced to depend on interfaces they do not use.

**Example (Violating ISP):**

```python
class Worker:
    def work(self):
        pass
  
    def eat(self):
        pass

class Robot(Worker):
    def work(self):
        print("Robot working")
  
    def eat(self):
        raise Exception("Robots don't eat!")
```

`Robot` should not be forced to implement `eat()`.

**Refactored Code (Following ISP using Separate Interfaces):**

```python
class Workable:
    def work(self):
        pass

class Eatable:
    def eat(self):
        pass

class Human(Workable, Eatable):
    def work(self):
        print("Human working")

    def eat(self):
        print("Human eating")

class Robot(Workable):
    def work(self):
        print("Robot working")
```

Now, classes implement only the methods they need.

---

### **7. How does the Dependency Inversion Principle promote decoupling in a system?**

**Answer:**

**Dependency Inversion Principle (DIP):** High-level modules should not depend on low-level modules; both should depend on abstractions.

**Example (Violating DIP):**

```python
class MySQLDatabase:
    def connect(self):
        return "Connected to MySQL"

class Application:
    def __init__(self):
        self.db = MySQLDatabase()
  
    def get_data(self):
        return self.db.connect()
```

Here, `Application` is tightly coupled to `MySQLDatabase`.

**Refactored Code (Following DIP using Abstraction):**

```python
from abc import ABC, abstractmethod

class Database(ABC):
    @abstractmethod
    def connect(self):
        pass

class MySQLDatabase(Database):
    def connect(self):
        return "Connected to MySQL"

class PostgreSQLDatabase(Database):
    def connect(self):
        return "Connected to PostgreSQL"

class Application:
    def __init__(self, db: Database):
        self.db = db
  
    def get_data(self):
        return self.db.connect()

app = Application(MySQLDatabase())  # Can switch databases easily
print(app.get_data())
```

Now, `Application` depends on an abstraction, making it flexible.

---

### **Scenario-Based Questions**

#### **8. If you have a class handling user authentication and logging, which principle is violated, and how would you fix it?**

**Answer:**

This violates **Single Responsibility Principle (SRP)** because authentication and logging are separate concerns.

**Solution:** Split into separate classes: `Authenticator` and `Logger`.

---

#### **9. How can you refactor a monolithic class into multiple classes following SOLID principles?**

**Answer:**

* Identify responsibilities and separate them (SRP).
* Use interfaces to avoid forcing methods on unrelated classes (ISP).
* Introduce abstraction to decouple dependencies (DIP).
* Use inheritance and composition properly to follow LSP.

---

#### **10. What would happen if we violate the Liskov Substitution Principle in an inheritance hierarchy?**

**Answer:**

* Code might break when replacing a base class with a subclass.
* Unexpected behavior could arise, leading to runtime errors.
* It reduces maintainability and increases debugging complexity.
