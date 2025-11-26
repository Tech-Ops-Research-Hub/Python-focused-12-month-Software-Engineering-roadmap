## **1. Object-Oriented Programming (OOP)**

**Why OOP exists:** Real-world systems have *things* (data) and *actions* (behavior). OOP packages them together so your program models the real world.

---

### **Classes**

* Blueprint for an object
* Defines properties (attributes) and actions (methods)

**Example:**

```python
class Book:
    def __init__(self, title, author, copies):
        self.title = title
        self.author = author
        self.copies = copies

    def borrow(self):
        if self.copies > 0:
            self.copies -= 1
            return True
        else:
            return False
```

* `__init__` sets up the object when created.
* `borrow()` changes the object’s state.

---

### **Inheritance**

* Lets one class take properties and methods from another class.
* Avoids rewriting code.

**Example:**

```python
class Item:
    def __init__(self, title):
        self.title = title

class Book(Item):
    def __init__(self, title, author):
        super().__init__(title)
        self.author = author
```

---

### **Encapsulation**

* Protect internal data from being changed by accident.
* Use “private” or “protected” variables (prefix `_`).

**Example:**

```python
class Account:
    def __init__(self, balance):
        self._balance = balance

    def deposit(self, amount):
        self._balance += amount

    def get_balance(self):
        return self._balance
```

---

## **2. Functional Python**

Python lets you treat functions as *first-class citizens*. You can pass them around, wrap them, and return them from other functions.

---

### **Lambda Functions**

* Short, one-line functions

```python
square = lambda x: x*x
print(square(5))  # 25
```

---

### **Closures**

* Function remembers variables from outside itself

```python
def multiplier(n):
    def inner(x):
        return x * n
    return inner

times_three = multiplier(3)
print(times_three(10))  # 30
```

---

### **Decorators**

* Add behavior to functions without changing them

```python
def log(func):
    def wrapper(*args, **kwargs):
        print("Running:", func.__name__)
        return func(*args, **kwargs)
    return wrapper

@log
def greet():
    print("Hello")

greet()
# Output:
# Running: greet
# Hello
```

---

# **Project (Weeks 5–6): Library Management System (CLI)**

**Goal:** Combine OOP + Functional Python into a small program where users can borrow and return books.

---

### **Entities**

1. **Book** — title, author, copies
2. **User** — name, borrowed books
3. **Library** — manages books and users

---

### **Example Classes**

```python
class Book:
    def __init__(self, title, author, copies):
        self.title = title
        self.author = author
        self.copies = copies

    def borrow(self):
        if self.copies > 0:
            self.copies -= 1
            return True
        return False

    def return_book(self):
        self.copies += 1


class User:
    def __init__(self, name):
        self.name = name
        self.borrowed = []

    def borrow_book(self, book):
        if book.borrow():
            self.borrowed.append(book.title)
        else:
            print("Book unavailable")


class Library:
    def __init__(self):
        self.books = {}
        self.users = {}

    def add_book(self, title, author, copies):
        self.books[title] = Book(title, author, copies)

    def register_user(self, name):
        self.users[name] = User(name)
```

---

### **CLI Menu Example**

```python
def menu():
    print("1. Add Book")
    print("2. Register User")
    print("3. Borrow Book")
    print("4. Return Book")
    print("5. View Books")
```

---

# **Assignments (Weeks 5–6)**

### **Assignment 1: OOP Practice**

* Create a `Vehicle` class with attributes like `brand`, `speed`.
* Inherit `Car` from `Vehicle` and add `fuel_type`.
* Demonstrate encapsulation by making `speed` protected.

---

### **Assignment 2: Functional Python**

* Write a lambda to filter even numbers from a list.
* Create a closure that multiplies any number by 5.
* Write a decorator to print `"Function started"` before a function runs.

---

### **Assignment 3: JSON Data**

* Save class instances (Book and User) to JSON file.
* Load JSON back and reconstruct objects.

---

### **Assignment 4: Library Project Enhancement**

* Search books by partial title.
* Prevent duplicate users.
* Track number of books each user borrowed.
* Log every operation with a decorator.
* Display analytics: total books, most borrowed book, number of active users.

---
