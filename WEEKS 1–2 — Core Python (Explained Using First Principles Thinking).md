# **WEEKS 1–2 — Core Python (Explained Using First Principles Thinking)**

**Objective:** Build Python knowledge from the ground up by understanding *why* each idea exists and *how* it works at the lowest level. No memorization. No surface learning. Just clean fundamentals that prepare the learner for real engineering work.

---

# **1. Variables, Data Types, and Operators (First Principles Breakdown)**

## **1.1 Why Variables Exist**

A computer’s memory is just a giant grid of empty boxes.
A variable is a *label* you attach to one of those boxes so you can store information and retrieve it later.

**Example:**

```
age = 21
```

This means:
– Find an empty box in memory.
– Put the number 21 in it.
– Attach the label “age” so you can refer to it again.

**Key Principle:**
A variable exists to *remember something* for later use.

---

## **1.2 Why Data Types Exist**

Different forms of data need different ways of being stored and processed.

A computer must know whether something is a number, text, or True/False before it can perform operations.

Main Python types:
– Numbers → for math
– Strings → for text
– Booleans → for decisions
– Lists/Tuples → for ordered groups
– Dicts → for key/value storage
– Sets → for uniqueness

**First Principle:**
A data type tells the computer *how to treat* the value stored in memory.

---

## **1.3 Why Operators Exist**

Operators are the minimal instructions you give the computer to transform or compare values.

Examples:
– `+` adds
– `*` multiplies
– `==` checks equality
– `in` checks membership

**First Principle:**
Operators are just tiny built-in programs designed to manipulate data efficiently.

---

# **2. Control Flow: Loops and Conditionals (First Principles Breakdown)**

## **2.1 Why Conditionals Exist**

A program must react differently based on different situations.

Example:

```
if score >= 50:
    print("Pass")
```

This means:
– Check a condition
– Choose one branch of execution
– Ignore the others

**First Principle:**
Conditionals exist because computers need a way to make decisions.

---

## **2.2 Why Loops Exist**

Repeating the same action manually is wasteful.
A loop tells the computer:
“Keep doing this until the condition changes.”

### For loop

Iterates over items in a sequence.
It’s useful when the number of repetitions is predictable.

### While loop

Repeats until a condition becomes false.
Useful when you don’t know the exact number of repetitions.

**First Principle:**
Loops exist to automate repetition with high precision.

---

# **3. Functions (First Principles Breakdown)**

## **3.1 Why Functions Exist**

When writing programs, repeating the same logic leads to errors and messy code.
A function extracts a piece of logic so it can be reused.

Example:

```
def add(a, b):
    return a + b
```

This means:
– Group the logic
– Name it
– Reuse it without rewriting it

**First Principle:**
Functions allow you to package logic into a single place, reducing duplication and increasing clarity.

---

## **3.2 Why Function Scope Exists**

Scope prevents different parts of your program from accidentally interfering with each other.

Variables inside a function are protected from the outside world.

**First Principle:**
Scope is protection — it isolates logic so variables don’t clash or leak.

---

## **3.3 Why Default Parameters Exist**

Some actions need flexible inputs.
If a value is missing, the function can use a fallback.

Example:

```
def greet(name="Guest"):
    return f"Hello {name}"
```

**First Principle:**
Defaults reduce friction by giving your function predictable behavior even when inputs are missing.

---

# **4. Modules and Packages (First Principles Breakdown)**

## **4.1 Why Modules Exist**

One large file becomes impossible to manage.
Breaking code into files creates organization and clarity.

**First Principle:**
A module is just a Python file that lets you group related logic.

---

## **4.2 Why Packages Exist**

As projects grow, you need folders to group many modules.
`__init__.py` tells Python: “This folder is a package.”

**First Principle:**
Packages provide structure for large codebases, preventing chaos.

---

# **5. Weeks 1–2 Project — Command-Line Calculator (Built From First Principles)**

A command-line calculator is the perfect early project because it forces you to apply all fundamentals at once.

---

## **5.1 First Principles Breakdown of a Calculator**

### What is a calculator?

A system that:

1. Accepts input
2. Processes it
3. Produces an output

This is the most basic structure of any software system.

### Why this project?

– It reinforces variables (store numbers)
– It reinforces data types (numbers vs strings)
– It reinforces operators (math)
– It reinforces conditionals (input validation)
– It reinforces functions (one function per operation)
– It reinforces modules (operations in separate files)

This is a miniature version of how APIs and microservices work.

---

# **6. Recommended Architecture (Explained from First Principles)**

```
calculator/
    app.py
    operations/
        add.py
        subtract.py
        multiply.py
        divide.py
        power.py
        modulus.py
    utils/
        validator.py
```

### Why this structure?

– `app.py` controls the flow → input → process → output
– `operations/` stores pure logic (modular, testable)
– `utils/validator.py` handles input validation so that operation files stay clean

**This mirrors how real backend systems are built:**
– Entry point
– Business logic layer
– Validation layer

---

# **7. Implementation Milestones (Weeks 1–2)**

## **Week 1 — Fundamentals + Initial Structure**

[ ] Master variables and data types
[ ] Practice arithmetic operations
[ ] Build the initial folder structure
[ ] Create `operations/` module files
[ ] Implement add, subtract, multiply, divide
[ ] Build validator for inputs

## **Week 2 — Expansion + Full Calculator**

[ ] Implement exponent and modulus
[ ] Add error handling for invalid input
[ ] Add clean user interaction in `app.py`
[ ] Test calculator with many inputs
[ ] Write a simple README
[ ] Push final version to GitHub

---

# **Summary (First Principles View)**

Everything in Weeks 1–2 revolves around one core idea:

### A computer is a machine that transforms input into output using logic you define.

Variables store the input.
Data types define the form.
Operators manipulate the form.
Conditionals guide the path.
Loops repeat actions.
Functions package logic.
Modules organize logic.
The calculator ties all of these into a coherent system.
