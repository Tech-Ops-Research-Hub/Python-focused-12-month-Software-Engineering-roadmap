# **Weeks 13–14: Advanced Algorithms & Optimization — Detailed Beginner-Friendly Guide**

**Goal:** Learn to solve complex problems efficiently, analyze algorithm performance, and build an **Algorithm Challenge Mini-Portfolio** showcasing mastery.

---

## **1. Dynamic Programming (DP)**

**Concept:**

* Solve problems by **breaking them into smaller overlapping subproblems** and storing the results to avoid repeated work.
* DP is a more efficient alternative to plain recursion for problems with repeated calculations.

---

### **1.1 Steps to Solve with DP**

1. **Define subproblem:** Identify smaller instances of the main problem.
2. **Find recurrence relation:** Express the solution in terms of subproblems.
3. **Decide storage method:**

   * **Memoization (Top-Down):** Store results during recursion
   * **Tabulation (Bottom-Up):** Fill a table iteratively

---

### **1.2 Example: Fibonacci Numbers**

**Recursive (Inefficient):**

```python
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)

print(fib(10))  # 55
```

**Memoization (Efficient):**

```python
memo = {}
def fib_memo(n):
    if n in memo:
        return memo[n]
    if n <= 1:
        memo[n] = n
    else:
        memo[n] = fib_memo(n-1) + fib_memo(n-2)
    return memo[n]

print(fib_memo(50))
```

**Tabulation (Bottom-Up):**

```python
def fib_tab(n):
    dp = [0, 1] + [0]*(n-1)
    for i in range(2, n+1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]

print(fib_tab(50))
```

**Tip:** DP = trading **memory for speed** by storing results.

---

### **1.3 Common DP Problems**

* Fibonacci / Tribonacci
* Knapsack Problem
* Coin Change Problem
* Longest Common Subsequence

---

## **2. Complexity Analysis (Big O)**

**Concept:** Measure how **runtime or memory usage grows** with input size.

### **Common Notations**

| Complexity | Example                | Description              |
| ---------- | ---------------------- | ------------------------ |
| O(1)       | Access element in list | Constant time            |
| O(n)       | Linear search          | Time grows linearly      |
| O(n²)      | Bubble sort            | Time grows quadratically |
| O(log n)   | Binary search          | Divide and conquer       |

**Why it matters:** Helps choose the **most efficient algorithm** for large inputs.

---

### **2.1 Examples**

**Linear Search:** O(n)

```python
for item in arr:
    if item == target:
        break
```

**Binary Search:** O(log n)

```python
def binary_search(arr, target):
    left, right = 0, len(arr)-1
    while left <= right:
        mid = (left+right)//2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

**Bubble Sort:** O(n²)

* Nested loops → grows quadratically with input size.

---

## **3. Project: Algorithm Challenge Mini-Portfolio**

**Goal:** Solve a set of algorithmic problems and document solutions to showcase **problem-solving + coding skills**.

---

### **3.1 Suggested Problems**

1. Fibonacci / Tribonacci sequence (DP)
2. Knapsack problem
3. Longest increasing subsequence
4. Coin change problem
5. Maze shortest path (optional BFS/DP combination)

### **3.2 File Structure**

```
algorithm_portfolio/
    fibonacci.py
    knapsack.py
    coin_change.py
    lis.py
    README.md
```

---

### **3.3 Example: 0/1 Knapsack (DP)**

```python
def knapsack(weights, values, W):
    n = len(weights)
    dp = [[0]*(W+1) for _ in range(n+1)]
    for i in range(1, n+1):
        for w in range(1, W+1):
            if weights[i-1] <= w:
                dp[i][w] = max(dp[i-1][w], dp[i-1][w-weights[i-1]] + values[i-1])
            else:
                dp[i][w] = dp[i-1][w]
    return dp[n][W]

weights = [1, 2, 3, 2]
values = [10, 20, 30, 40]
W = 5
print(knapsack(weights, values, W))  # Output: 60
```

**Explanation:**

* dp[i][w] = max value with first i items and weight ≤ w
* Bottom-up approach avoids recomputation

---

### **3.4 Optimization Tips**

* Avoid nested loops if possible
* Use memoization to save repeated computation
* Precompute values for multiple queries

---

## **4. Assignments (Weeks 13–14)**

### **Assignment 1: Dynamic Programming**

1. Fibonacci sequence with memoization and tabulation
2. Longest common subsequence of two strings
3. Coin change problem

### **Assignment 2: Complexity Analysis**

1. Write 3 sorting algorithms (bubble, insertion, merge)
2. Calculate their Big O
3. Test with lists of increasing sizes

### **Assignment 3: Mini-Portfolio**

1. Solve 5 algorithm challenges
2. Document approach in README.md
3. Include code, input/output, and complexity notes

---

**Outcome:** By the end of Weeks 13–14, learners will:

* Solve complex problems efficiently with DP and memoization
* Analyze algorithms with Big O notation
* Build a portfolio of solved algorithmic problems to showcase skills

---

