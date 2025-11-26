# **Phase 3: Backend Development with Python (Weeks 15–18: FastAPI Basics)**

This phase introduces **backend development using FastAPI**, focusing on building REST APIs, validating data, handling HTTP requests, and completing a **Blog API project**. All explanations and assignments are designed to be beginner-friendly but comprehensive enough for real-world application.

---

## **1. FastAPI Setup & Environment**

### **1.1 Install Dependencies**

```bash
pip install fastapi uvicorn
```

* **FastAPI:** Python framework for building APIs quickly
* **Uvicorn:** ASGI server to run FastAPI applications

### **1.2 Project Structure**

```
blog_api/
│
├─ main.py        # Entry point for the FastAPI app
├─ models.py      # Pydantic models for validation
├─ routers/
│   └─ posts.py   # Routes for blog operations
└─ database.py    # Optional DB integration for later phases
```

---

## **2. FastAPI Application Basics**

### **2.1 Creating a FastAPI App**

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello World"}
```

* **`@app.get("/")`**: Decorator that maps HTTP GET requests to this function
* **`read_root()`**: Function returning a JSON response

### **2.2 Running the App**

```bash
uvicorn main:app --reload
```

* **`--reload`** automatically reloads the server on code changes
* Visit `http://127.0.0.1:8000` in a browser to test

---

## **3. CRUD Operations (REST API)**

**CRUD:** Create, Read, Update, Delete

### **3.1 Pydantic Models for Validation**

```python
from pydantic import BaseModel, Field

class Post(BaseModel):
    id: int
    title: str = Field(..., min_length=3, max_length=50)
    content: str
```

* Ensures **correct types and constraints** for incoming data
* Returns **400 error automatically** if validation fails

---

### **3.2 CRUD Endpoints**

#### **Create Post**

```python
@app.post("/posts/")
def create_post(post: Post):
    posts.append(post)
    return post
```

#### **Read Posts**

```python
@app.get("/posts/")
def get_posts():
    return posts

@app.get("/posts/{post_id}")
def get_post(post_id: int):
    for post in posts:
        if post.id == post_id:
            return post
    return {"error": "Post not found"}
```

#### **Update Post**

```python
@app.put("/posts/{post_id}")
def update_post(post_id: int, updated_post: Post):
    for i, post in enumerate(posts):
        if post.id == post_id:
            posts[i] = updated_post
            return updated_post
    return {"error": "Post not found"}
```

#### **Delete Post**

```python
@app.delete("/posts/{post_id}")
def delete_post(post_id: int):
    for i, post in enumerate(posts):
        if post.id == post_id:
            posts.pop(i)
            return {"message": "Deleted"}
    return {"error": "Post not found"}
```

---

## **4. Path & Query Parameters**

### **4.1 Path Parameters**

* Specify resource directly in the URL

```python
@app.get("/users/{user_id}")
def get_user(user_id: int):
    return {"user_id": user_id}
```

### **4.2 Query Parameters**

* Optional filters or limits

```python
@app.get("/users/")
def get_users(skip: int = 0, limit: int = 10):
    return {"skip": skip, "limit": limit}
```

---

## **5. Project: Blog API**

### **5.1 Features**

1. CRUD operations for blog posts
2. Input validation (Pydantic)
3. In-memory storage (Python list)
4. Optional: query search by title or content

### **5.2 Suggested Structure**

```
blog_api/
├─ main.py
├─ models.py
├─ routers/posts.py
└─ database.py
```

### **5.3 Development Steps**

1. Set up FastAPI project and main.py
2. Create Post model in models.py
3. Implement CRUD endpoints in routers/posts.py
4. Add validation and query parameters
5. Test endpoints using **Swagger UI** (`http://127.0.0.1:8000/docs`)

---

## **6. Assignments (Weeks 15–18)**

### **Assignment 1: FastAPI Fundamentals**

* Create a `/hello` endpoint returning your name
* Create a `/status` endpoint returning `{"status": "Running"}`

### **Assignment 2: Blog API CRUD**

* Implement **Create**, **Read**, **Update**, **Delete** endpoints for posts
* Include input validation: title (3–50 characters), content (non-empty)
* Test endpoints using Swagger UI

### **Assignment 3: Path & Query Parameters**

* Add `/posts/{post_id}` to fetch a single post by ID
* Add `/posts/?skip=0&limit=5` to return limited posts
* Add optional query parameter to search posts by title keyword

### **Assignment 4: Mini Enhancements**

* Add timestamp (`created_at`) for posts
* Implement simple in-memory authentication (optional)
* Add sorting by creation date or title using query parameters

**All assignments should:**

* Include proper Pydantic validation
* Be tested via Swagger UI
* Be stored in GitHub repository with commits for each milestone

---

## **7. Learning Outcomes (Weeks 15–18)**

By the end of this phase, learners will be able to:

* Set up FastAPI and run a development server
* Create RESTful APIs with CRUD functionality
* Use **path and query parameters** for dynamic data access
* Implement **Pydantic validation** for input data
* Build and test a structured Blog API project
* Apply Git version control for backend projects

---
