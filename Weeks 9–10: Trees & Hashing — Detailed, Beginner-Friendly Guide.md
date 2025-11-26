# **Weeks 9–10: Trees & Hashing — Detailed, Beginner-Friendly Guide**

**Goal:** Understand hierarchical and hashed data structures in Python, their real-world applications, and implement a fully functional **Phonebook CLI app**.

---

## **1. Trees**

**Concept:** A tree is a way to organize data hierarchically, like a family tree or folder system. Each **node** contains data and can point to **child nodes**.

* **Root:** Topmost node
* **Leaf:** Node with no children
* **Parent / Child:** Standard hierarchical relationships

---

### **Binary Tree**

* Each node can have **at most two children** (left and right).
* Useful for structured data storage and traversal operations.

**Python Implementation:**

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
```

**Inserting Nodes:**

```python
root = Node(10)
root.left = Node(5)
root.right = Node(15)
```

---

### **Binary Search Tree (BST)**

* Left child < parent
* Right child > parent
* Efficient for searching, inserting, and deleting items.

**Insertion Function:**

```python
def insert(root, value):
    if root is None:
        return Node(value)
    if value < root.value:
        root.left = insert(root.left, value)
    else:
        root.right = insert(root.right, value)
    return root
```

**Search Function:**

```python
def search(root, key):
    if root is None or root.value == key:
        return root
    if key < root.value:
        return search(root.left, key)
    return search(root.right, key)
```

---

### **Tree Traversals**

Traversing means visiting each node in a specific order.

1. **In-order:** left → root → right → gives sorted order for BST
2. **Pre-order:** root → left → right → useful for copying tree structure
3. **Post-order:** left → right → root → useful for deleting nodes

**Example: In-order Traversal**

```python
def inorder(root):
    if root:
        inorder(root.left)
        print(root.value)
        inorder(root.right)
```

---

## **2. Hashing**

**Concept:** Hashing allows fast access to data using a **key → value** pair, like looking up a phone number by a person’s name.

* **Hash Map:** Python `dict`
* **Set:** Store unique items, fast membership checking

**Hash Map Example:**

```python
phonebook = {}
phonebook["Alice"] = "0712345678"
phonebook["Bob"] = "0723456789"
print(phonebook["Alice"])  # Output: 0712345678
```

**Set Example:**

```python
unique_numbers = set([1, 2, 3, 2])
print(unique_numbers)  # Output: {1, 2, 3}
```

**Why Hashing?**

* Searching for a name in a list is slow (O(n))
* Hashing gives **constant time lookup** (O(1))

---

## **3. Combining Trees & Hashing**

* **BST** → maintain alphabetical order for listing contacts
* **Hash Map** → lookup numbers quickly by name

**Design Principle:** Use each structure for its strength:

* BST → sorted view
* Hash map → instant search

---

## **4. Phonebook CLI App (Project)**

**Goal:** Apply trees and hash maps to build a real-world CLI application.

---

### **Features**

1. Add contacts (name → phone number)
2. Search by name quickly (hash map)
3. List contacts alphabetically (BST traversal)
4. Update and delete contacts
5. Save/load contacts from file (`contacts.json`)

---

### **File Structure**

```
phonebook/
    phonebook.py    # main program
    contacts.json   # persistent storage
    utils.py        # helper functions
```

---

### **Python Implementation Snippets**

**1. BST Node Class**

```python
class BSTNode:
    def __init__(self, name, number):
        self.name = name
        self.number = number
        self.left = None
        self.right = None
```

**2. Inserting into BST**

```python
def insert_bst(root, name, number):
    if root is None:
        return BSTNode(name, number)
    if name < root.name:
        root.left = insert_bst(root.left, name, number)
    else:
        root.right = insert_bst(root.right, name, number)
    return root
```

**3. Searching BST**

```python
def search_bst(root, name):
    if root is None or root.name == name:
        return root
    if name < root.name:
        return search_bst(root.left, name)
    return search_bst(root.right, name)
```

**4. Hash Map for Fast Lookup**

```python
contacts = {}
def add_contact(name, number):
    contacts[name] = number

def search_contact(name):
    return contacts.get(name, "Contact not found")
```

**5. In-order Traversal for Sorted Listing**

```python
def inorder(root):
    if root:
        inorder(root.left)
        print(root.name, root.number)
        inorder(root.right)
```

**6. File I/O (Saving & Loading)**

```python
import json

def save_contacts():
    with open("contacts.json", "w") as f:
        json.dump(contacts, f, indent=2)

def load_contacts():
    global contacts
    try:
        with open("contacts.json") as f:
            contacts = json.load(f)
    except FileNotFoundError:
        contacts = {}
```

---

## **5. Assignments (Weeks 9–10)**

### **Assignment 1: Binary Tree Practice**

1. Create a binary tree with 10 nodes.
2. Implement in-order, pre-order, and post-order traversals.
3. Count the number of nodes and calculate tree height.

### **Assignment 2: Binary Search Tree**

1. Insert numbers or names into BST.
2. Implement search to find a specific value.
3. Delete a node and print updated traversal.

### **Assignment 3: Hashing**

1. Implement a phonebook using Python dictionary.
2. Add, search, update, delete contacts.
3. Use a set to track unique phone numbers.

### **Assignment 4: Phonebook CLI App**

1. Combine BST and hash map for the project.
2. CLI menu: Add, Search, List (sorted), Update, Delete, Exit.
3. Save/load contacts using JSON.
4. Optional: implement undo for last operation using stack.

---

**Outcome:** By the end of Weeks 9–10, learners will:

* Understand hierarchical and hashed data structures
* Implement and traverse trees and BSTs
* Use hash maps for fast lookups
* Combine multiple data structures in a functional CLI app
* Build a project that models a real-world phonebook system efficiently

---

