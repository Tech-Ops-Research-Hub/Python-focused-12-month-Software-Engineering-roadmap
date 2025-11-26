# **Weeks 7–8: Linear Data Structures — Beginner-Friendly Guide**

**Goal:** Learn how to store and manage sequences of items in Python. Build a simple Task Scheduler to practice.

---

## **1. Lists**

* **What it is:** A list is a sequence of items, like a shopping list.
* **Why use it:** You can add, remove, or change items anytime.

**Example:**

```python
tasks = ["code", "debug", "commit"]
tasks.append("push")  # add a task
tasks.pop(1)           # remove 'debug'
print(tasks)           # ['code', 'commit', 'push']
```

---

## **2. Stacks (LIFO)**

* **What it is:** Stack = Last-In-First-Out. The last item added is the first to come out.
* **Use:** Undo actions, browser history, call stack.

**Example:**

```python
stack = []
stack.append("task1")  # push
stack.append("task2")
top = stack.pop()      # removes 'task2'
print(stack)           # ['task1']
```

**Tip:** Think of a stack as a pile of books; you can only take the top one.

---

## **3. Queues (FIFO)**

* **What it is:** Queue = First-In-First-Out. The first item added is the first to come out.
* **Use:** Print jobs, task scheduling, waiting lines.

**Example using `deque`:**

```python
from collections import deque

queue = deque()
queue.append("task1")   # enqueue
queue.append("task2")
first = queue.popleft()  # dequeue
print(queue)             # deque(['task2'])
```

**Tip:** Think of a queue as a line at the supermarket.

---

## **4. Arrays**

* **What it is:** An array stores items of the same type in order.
* **Why use it:** Fast access to items by position.
* **Python tip:** Regular lists work as dynamic arrays; use `array` or `numpy` for numbers.

**Example:**

```python
import array
numbers = array.array("i", [1, 2, 3])
numbers.append(4)
print(numbers)  # array('i', [1, 2, 3, 4])
```

---

## **5. Searching**

* **Linear Search:** Look at each item until you find it.

```python
def linear_search(arr, target):
    for i, val in enumerate(arr):
        if val == target:
            return i
    return -1
```

* **Binary Search:** Fast search in a sorted list by checking the middle.

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

**Tip:** Linear = check one by one. Binary = split the list in half each time.

---

## **6. Sorting**

* **Bubble Sort:** Compare neighbors and swap to order the list.

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
```

* **Insertion Sort:** Build a sorted list by inserting each item in the correct place.

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i-1
        while j >=0 and arr[j] > key:
            arr[j+1] = arr[j]
            j -= 1
        arr[j+1] = key
```

**Tip:** Sorting = arranging items so we can find or process them easily.

---

## **7. Project: Task Scheduler CLI**

**Goal:** Practice lists, stacks, queues, sorting, and file I/O.

**Features:**

1. Add tasks (FIFO queue).
2. Complete tasks (pop from stack to undo).
3. List all tasks.
4. Sort tasks by priority or due date.
5. Save and load tasks from a file.

**Suggested Structure:**

```
task_scheduler/
    scheduler.py  # main program
    tasks.json    # store tasks
    utils.py      # helper functions
```

**First Principles:**

* **Queue** → task order
* **Stack** → undo completed tasks
* **List** → manipulate tasks in memory
* **File I/O** → save tasks permanently

---

## **Assignments**

### **Assignment 1: Linear Structures**

1. Create a stack class with `push`, `pop`, `peek`.
2. Create a queue class with `enqueue`, `dequeue`, `peek`.
3. Reverse a list using a stack.

### **Assignment 2: Searching**

1. Linear search for a name in a list.
2. Binary search for a number in a sorted list.
3. Compare the time it takes for each search on 1000 items.

### **Assignment 3: Sorting**

1. Implement bubble sort and insertion sort.
2. Sort tasks by priority and by name.

### **Assignment 4: Task Scheduler**

1. Build a CLI program to add, remove, list, complete tasks.
2. Save tasks to a file and reload on startup.
3. Use queue for tasks and stack for recently completed tasks.

---
