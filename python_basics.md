# Basic Python Questions

1. **What is Python?**

   - **Answer:** Python is a high-level, interpreted programming language known for its easy-to-read syntax and dynamic semantics. It supports multiple programming paradigms, including procedural, object-oriented, and functional programming.
2. **What are the key features of Python?**

   - **Answer:** Some key features of Python include:
     - Easy-to-read syntax
     - Interpreted language
     - Dynamic typing
     - Memory management
     - Extensive standard library
     - Support for multiple programming paradigms
     - Strong community support
3. **What is PEP 8 and why is it important?**

   - **Answer:** PEP 8 is the Python Enhancement Proposal that provides guidelines and best practices on how to write Python code. It is important because it ensures code readability and consistency, making it easier for teams to collaborate and maintain codebases.
4. **What is the difference between `list` and `tuple` in Python?**

   - **Answer:** The main differences are:
     - **Lists** are mutable (can be modified) and use square brackets `[]`.
     - **Tuples** are immutable (cannot be modified) and use parentheses `()`.
5. **How is memory managed in Python?**

   - **Answer:** Python uses automatic memory management, which includes garbage collection to reclaim unused memory. Python's memory manager allocates heap space for objects and automatically handles reference counting and cyclic garbage collection.
6. **What are Python decorators and how are they used?**

   - **Answer:** Decorators are a way to modify or enhance functions or methods without changing their actual code. They are implemented as functions (or classes) that return a function. They are often used to add functionality like logging, access control, or instrumentation.
     ```python
     def my_decorator(func):
         def wrapper():
             print("Something is happening before the function is called.")
             func()
             print("Something is happening after the function is called.")
         return wrapper

     @my_decorator
     def say_hello():
         print("Hello!")

     say_hello()
     ```
7. **What is the difference between `==` and `is` in Python?**

   - **Answer:** `==` checks for value equality (whether two objects have the same value), whereas `is` checks for identity equality (whether two objects are the same instance in memory).

### Data Structures and Algorithms

1. **Explain different types of data structures available in Python.**

   - **Answer:** Python provides several built-in data structures, including:
     - **Lists:** Ordered, mutable collections.
     - **Tuples:** Ordered, immutable collections.
     - **Dictionaries:** Key-value pairs, unordered.
     - **Sets:** Unordered collections of unique elements.
2. **How would you implement a stack and a queue in Python?**

   - **Answer:**
     ```python
     # Stack using list
     stack = []
     stack.append(1)  # Push
     stack.pop()      # Pop

     # Queue using collections.deque
     from collections import deque
     queue = deque()
     queue.append(1)  # Enqueue
     queue.popleft()  # Dequeue
     ```
3. **Write a Python program to check if a string is a palindrome.**

   - **Answer:**
     ```python
     def is_palindrome(s):
         return s == s[::-1]

     print(is_palindrome("racecar"))  # True
     print(is_palindrome("hello"))    # False
     ```
4. **How do you reverse a list in Python?**

   - **Answer:** You can reverse a list using slicing, the `reverse()` method, or the `reversed()` function.
     ```python
     my_list = [1, 2, 3, 4, 5]

     # Using slicing
     reversed_list = my_list[::-1]

     # Using reverse() method
     my_list.reverse()

     # Using reversed() function
     reversed_list = list(reversed(my_list))
     ```

### Object-Oriented Programming

1. **Explain the concepts of classes and objects in Python.**

   - **Answer:** A class is a blueprint for creating objects. It defines attributes and methods that the objects created from the class will have. An object is an instance of a class.
     ```python
     class Dog:
         def __init__(self, name, age):
             self.name = name
             self.age = age

         def bark(self):
             print("Woof!")

     my_dog = Dog("Buddy", 3)
     my_dog.bark()  # Outputs: Woof!
     ```
2. **What are the differences between instance variables and class variables?**

   - **Answer:** Instance variables are unique to each instance of a class and are defined within the `__init__` method. Class variables are shared among all instances of a class and are defined within the class but outside any methods.
3. **What are inheritance and polymorphism in Python?**

   - **Answer:** Inheritance allows a class to inherit attributes and methods from another class. Polymorphism allows methods to be used interchangeably between classes, typically through method overriding.
     ```python
     class Animal:
         def speak(self):
             pass

     class Dog(Animal):
         def speak(self):
             return "Woof!"

     class Cat(Animal):
         def speak(self):
             return "Meow!"

     animals = [Dog(), Cat()]
     for animal in animals:
         print(animal.speak())
     ```
4. **How do you handle exceptions in Python?**

   - **Answer:** Exceptions in Python are handled using try-except blocks.
     ```python
     try:
         result = 10 / 0
     except ZeroDivisionError:
         print("You can't divide by zero!")
     ```

### File Handling

1. **How do you read and write files in Python?**

   - **Answer:** You can use the `open()` function to read and write files.
     ```python
     # Reading a file
     with open('file.txt', 'r') as file:
         content = file.read()

     # Writing to a file
     with open('file.txt', 'w') as file:
         file.write("Hello, World!")
     ```
2. **What is the difference between `read()` and `readlines()`?**

   - **Answer:** `read()` reads the entire file as a single string, while `readlines()` reads the file and returns a list of strings, where each string is a line from the file.
3. **How do you handle file exceptions in Python?**

   - **Answer:** You handle file exceptions using try-except blocks.
     ```python
     try:
         with open('file.txt', 'r') as file:
             content = file.read()
     except FileNotFoundError:
         print("File not found!")
     ```

### Libraries and Frameworks

1. **What is NumPy and why is it used?**

   - **Answer:** NumPy is a library for numerical computing in Python. It provides support for arrays, matrices, and many mathematical functions to operate on these data structures. It is used for scientific computing and data analysis.
2. **Explain the use of pandas in Python.**

   - **Answer:** pandas is a library used for data manipulation and analysis. It provides data structures like Series (one-dimensional) and DataFrame (two-dimensional) to work with structured data easily. It is widely used for data cleaning, transformation, and analysis.
3. **What are some popular web frameworks in Python?**

   - **Answer:** Some popular web frameworks in Python are:
     - **Django:** A high-level framework that encourages rapid development and clean, pragmatic design.
     - **Flask:** A micro-framework that is lightweight and easy to extend.

### Practical Problems

1. **Write a Python program to find the factorial of a number.**

   - **Answer:**
     ```python
     def factorial(n):
         if n == 0:
             return 1
         else:
             return n * factorial(n-1)

     print(factorial(5))  # Outputs: 120
     ```
2. **Write a Python function to merge two dictionaries.**

   - **Answer:**
     ```python
     def merge_dicts(dict1, dict2):
         return {**dict1, **dict2}

     dict1 = {'a': 1, 'b': 2}
     dict2 = {'b': 3, 'c': 4}
     merged_dict = merge_dicts(dict1, dict2)
     print(merged_dict)  # Outputs: {'a': 1, 'b': 3, 'c': 4}
     ```
3. **Write a Python program to count the number of occurrences of each word in a given text file.**

   - **Answer:**
     ```python
     from collections import Counter

     def count_words(filename):
         with open(filename, 'r') as file:
             words = file.read().split()
             word_counts = Counter(words)
             return word_counts

     word_counts = count_words('file.txt')
     print(word_counts)
     ```
4. **Write a Python function to check if a number is prime.**

   - **Answer:**
     ```python
     def is_prime(n):
         if n <= 1:
             return False
         for i in range(2, int(n**2) + 1):
             if n % i == 0:
                 return False
         return True

     print(is_prime(5))

     ```

# Outputs: True

    print(is_prime(10))  # Outputs: False
     ```

### Advanced Topics (if applicable)

1. **Explain the concept of generators in Python.**

   - **Answer:** Generators are functions that return an iterable set of items, one at a time, in a special way. They are written using the `yield` statement instead of `return`. Generators are used to create iterators with a simple and concise syntax.
     ```python
     def my_generator():
         yield 1
         yield 2
         yield 3

     for value in my_generator():
         print(value)
     ```
2. **What is a lambda function? How is it used?**

   - **Answer:** A lambda function is an anonymous function defined using the `lambda` keyword. It can take any number of arguments but has only one expression. It is often used for short, simple functions.
     ```python
     add = lambda x, y: x + y
     print(add(3, 5))  # Outputs: 8
     ```
3. **Explain the concept of list comprehension with an example.**

   - **Answer:** List comprehension is a concise way to create lists. It consists of brackets containing an expression followed by a for clause and zero or more if clauses.
     ```python
     squares = [x**2 for x in range(10)]
     print(squares)  # Outputs: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
     ```

### Behavioral Questions

1. **Can you describe a Python project you have worked on?**

   - **Answer:** The candidate should provide details about a Python project they have worked on, including the problem it solved, the technologies used, and their role in the project.
2. **How do you approach debugging in Python?**

   - **Answer:** The candidate might mention using print statements, logging, the `pdb` module, or IDE/debugger tools to trace and fix issues in their code.
3. **What resources do you use to learn and improve your Python skills?**

   - **Answer:** The candidate might mention online courses, books, documentation, coding practice sites like LeetCode or HackerRank, and community resources like Stack Overflow and GitHub.
