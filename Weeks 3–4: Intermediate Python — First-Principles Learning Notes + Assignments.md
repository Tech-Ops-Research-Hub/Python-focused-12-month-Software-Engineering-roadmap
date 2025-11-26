## **1. Compound Data Structures (Lists, Tuples, Dictionaries, Sets)**

Core principle: software = structured data + transformations. These four structures cover 90% of data-handling problems.

---

### **Lists**

Ordered, resizable sequences.

**Use-case logic:** you choose a list when the order matters or items will change over time.

**Example:**

```python
students = ["Amina", "Brian", "Chao"]
students.append("Derrick")
students[1] = "Bree"
```

---

### **Tuples**

Ordered, fixed sequences.

**Use-case logic:** choose a tuple when the data must remain unchanged.

**Example:**

```python
location = (1.28, 36.82)
```

---

### **Dictionaries**

Key → value mappings.

**Use-case logic:** choose a dict when you need named data or fast lookup.

**Example:**

```python
profile = {"name": "Zuri", "role": "developer"}
profile["role"] = "engineer"
```

---

### **Sets**

Unordered unique values.

**Use-case logic:** choose a set when you need fast membership checking or deduplication.

**Example:**

```python
tech = {"python", "api", "backend"}
tech.add("python")  # ignored
```

---

## **2. List Comprehensions & Generators**

Core principle: transform sequences with minimal mental and memory load.

### **List Comprehension**

Builds a full list immediately.

```python
evens = [x for x in range(20) if x % 2 == 0]
```

### **Generator Expression**

Produces items lazily; memory-efficient for large streams.

```python
evens_gen = (x for x in range(1_000_000) if x % 2 == 0)
```

---

## **3. File I/O**

Core principle: persistent storage = bytes written to disk.

### **Read Whole File**

```python
with open("notes.txt", "r") as f:
    text = f.read()
```

### **Write File**

```python
with open("output.txt", "w") as f:
    f.write("Session logged")
```

### **Process Line-by-Line**

```python
with open("big.txt") as f:
    for line in f:
        handle(line)
```

---

## **4. Exceptions**

Core principle: errors are disruptions; handling = controlled recovery.

### **Basic Handling**

```python
try:
    age = int("22a")
except ValueError:
    age = 0
```

### **Cleanup with `finally`**

```python
try:
    f = open("data.txt")
    process(f)
finally:
    f.close()
```

---

## **5. Debugging**

Core principle: debugging = validating assumptions against actual program state.

### **Print Debugging**

```python
print("balance =", balance)
```

### **pdb**

```python
import pdb; pdb.set_trace()
```

### **VS Code Debugger**

Breakpoints → inspect variables → step execution.

---

# **Primary Project (Weeks 3–4): Personal Expense Tracker**

Purpose: apply intermediate Python by building a real system with storage, aggregation, exceptions, and data structures.

---

## **Project Requirements**

### Functional

* Add expenses: amount, category, date
* List all expenses
* Show totals by category
* Store data in JSON
* Load data on startup
* Handle invalid inputs gracefully

### Structure

```
expense_tracker/
    ├── tracker.py
    ├── data.json
    └── utils.py
```

### Data Model

```python
{
  "amount": 1200.0,
  "category": "transport",
  "date": "2025-11-26"
}
```

---

## **Core Operations (Examples)**

### Load Data

```python
def load_expenses():
    try:
        with open("data.json") as f:
            return json.load(f)
    except FileNotFoundError:
        return []
```

### Save Data

```python
def save_expenses(expenses):
    with open("data.json", "w") as f:
        json.dump(expenses, f, indent=2)
```

### Add Expense

```python
def add_expense(expenses):
    try:
        amount = float(input("Amount: "))
        category = input("Category: ")
        date = input("Date (YYYY-MM-DD): ")

        expenses.append({
            "amount": amount,
            "category": category,
            "date": date,
        })
    except ValueError:
        print("Invalid amount entered.")
```

### Total by Category

```python
def total_by_category(expenses):
    totals = {}
    for exp in expenses:
        cat = exp["category"]
        totals[cat] = totals.get(cat, 0) + exp["amount"]
    return totals
```

---

# **Assignments (Weeks 3–4)**

## **Assignment 1: Data Structures Mastery**

Implement the following without searching the internet:

1. Convert a list of numbers into a dictionary of
   `{ "even": [...], "odd": [...] }`.
2. Remove duplicates from a list *without* using `set()`.
3. Store student names in a tuple and try modifying one element.
   Document the error and explain it.
4. Create a set from user-entered words and report the count of unique words.

---

## **Assignment 2: File I/O**

Build a script called `notes.py` that:

* Lets a user add a note
* Saves it to `notes.txt`
* Lets the user read all notes
* Ensures the file is created automatically if missing
* Handles exceptions for invalid actions

---

## **Assignment 3: Exceptions & Debugging**

Write a program that:

* Asks the user for two numbers
* Performs division
* Handles division by zero
* Logs every step using print debugging
* Add `pdb.set_trace()` at one point to inspect variables

---

## **Assignment 4: Expense Tracker Enhancements**

Add these features to your main project:

* Search expenses by category
* Delete an expense by index
* Export a summary to a `.txt` file
* Add input validation for date format
* Add a simple error log file (`errors.log`)

---
