# **Weeks 11–12: Graphs & Recursion — Detailed, Beginner-Friendly Guide**

**Goal:** Learn how to represent relationships between objects, traverse connected structures efficiently, and solve problems recursively. Apply concepts to build a **Maze Solver CLI** project.

---

## **1. Graphs**

**Concept:** A graph is a collection of **nodes (vertices)** connected by **edges**.

* **Vertices (nodes):** Entities or points
* **Edges:** Connections between nodes

**Use Cases:** Social networks, maps, dependency resolution, network routing.

---

### **1.1 Graph Representation**

Two common ways to store a graph in Python:

1. **Adjacency List (Preferred in Python)**

* Dictionary where key = node, value = list of neighbors

```python
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}
```

2. **Adjacency Matrix**

* 2D list where `matrix[i][j] = 1` if edge exists, else 0

```python
matrix = [
    [0, 1, 1, 0, 0, 0],  # A
    [1, 0, 0, 1, 1, 0],  # B
    [1, 0, 0, 0, 0, 1],  # C
    [0, 1, 0, 0, 0, 0],  # D
    [0, 1, 0, 0, 0, 1],  # E
    [0, 0, 1, 0, 1, 0]   # F
]
```

---

### **1.2 Graph Traversal**

**Purpose:** Visit all nodes in a systematic way.

1. **Breadth-First Search (BFS)** – explore neighbors first, level by level

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    
    while queue:
        node = queue.popleft()
        if node not in visited:
            print(node)
            visited.add(node)
            queue.extend([n for n in graph[node] if n not in visited])
```

2. **Depth-First Search (DFS)** – explore as far as possible along a branch before backtracking

```python
def dfs(graph, node, visited=None):
    if visited is None:
        visited = set()
    visited.add(node)
    print(node)
    for neighbor in graph[node]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)
```

**Tip:** BFS = shortest path in unweighted graph, DFS = path exploration or topological sorting.

---

## **2. Recursion**

**Concept:** A function calls itself to solve a smaller version of the same problem.

**Structure:**

```python
def recursive_function(params):
    if base_case_condition:
        return result
    else:
        return recursive_function(smaller_problem)
```

**Example: Factorial**

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n-1)

print(factorial(5))  # 120
```

**First Principles:** Solve complex problems by **breaking them into smaller, identical subproblems**.

---

### **2.1 Divide-and-Conquer**

* Split problem → solve subproblems → combine results
* Examples: Merge Sort, Quick Sort, Binary Search, Graph traversal

---

## **3. Project: Maze Solver CLI**

**Goal:** Apply graph traversal and recursion to find a path through a maze.

---

### **3.1 Maze Representation**

* 2D grid where:

  * `0` = open path
  * `1` = wall

```python
maze = [
    [0, 1, 0, 0, 0],
    [0, 1, 0, 1, 0],
    [0, 0, 0, 1, 0],
    [1, 1, 0, 1, 0],
    [0, 0, 0, 0, 0]
]
```

* Start: `(0, 0)`
* End: `(4, 4)`

---

### **3.2 Solving with Recursion (DFS)**

```python
def solve_maze(maze, x, y, path=[]):
    rows, cols = len(maze), len(maze[0])
    if x < 0 or x >= rows or y < 0 or y >= cols or maze[x][y] == 1:
        return False
    path.append((x, y))
    if (x, y) == (rows-1, cols-1):
        return True
    maze[x][y] = 1  # mark as visited
    if (solve_maze(maze, x+1, y, path) or
        solve_maze(maze, x-1, y, path) or
        solve_maze(maze, x, y+1, path) or
        solve_maze(maze, x, y-1, path)):
        return True
    path.pop()
    return False

path = []
if solve_maze(maze, 0, 0, path):
    print("Path found:", path)
else:
    print("No path exists")
```

**Explanation:**

* Recursively try all directions
* Backtrack if path blocked
* Stop when the end is reached

---

### **3.3 Enhancements**

* Implement BFS to find **shortest path**
* Display maze and path visually in terminal
* Allow user to input maze size or custom walls

---

## **4. Assignments (Weeks 11–12)**

### **Assignment 1: Graph Basics**

1. Represent a small social network using adjacency list.
2. Traverse using BFS and DFS.
3. Count the number of connected components.

### **Assignment 2: Recursion**

1. Fibonacci sequence using recursion
2. Factorial
3. Sum of digits of a number

### **Assignment 3: Divide-and-Conquer**

1. Implement merge sort recursively
2. Solve a small pathfinding problem recursively

### **Assignment 4: Maze Solver**

1. Create a maze in a 2D grid
2. Solve with DFS recursion
3. Optional: Solve with BFS for shortest path
4. Print the path as list of coordinates

---

**Outcome:** By the end of Weeks 11–12, learners will:

* Represent complex relationships using graphs
* Traverse graphs efficiently (BFS/DFS)
* Solve problems recursively and apply divide-and-conquer
* Build a fully functional **Maze Solver CLI** project

---
