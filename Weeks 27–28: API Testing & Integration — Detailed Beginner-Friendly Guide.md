# **Weeks 27–28: API Testing & Integration — Detailed Guide**

This phase ensures that learners **validate, maintain, and professionalize their APIs**. The focus is on **manual and automated testing, logging, error handling, and documentation**. The culmination is a **full-featured Blog/Dashboard API**.

---

## **1. Postman for Manual API Testing**

**Purpose:** Test endpoints for correct behavior before automated tests.

### **1.1 Setup**

* Download Postman: [https://www.postman.com/downloads/](https://www.postman.com/downloads/)
* Create a **workspace** for your project

### **1.2 Testing Workflow**

1. Create **collection** for endpoints
2. Add requests for `GET`, `POST`, `PUT`, `DELETE`
3. Set **environment variables**: base URL, authentication tokens
4. Validate:

   * Correct HTTP status codes
   * JSON structure
   * Authentication behavior

**Example:** Testing Blog Post creation

```
POST /posts/
Body (JSON):
{
    "title": "First Post",
    "content": "Hello World",
    "author_id": 1
}
Expected response: 201 Created with post data
```

### **1.3 Automated Request Tests in Postman**

* Add **tests** under "Tests" tab:

```javascript
pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});
pm.test("Response has title", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("title");
});
```

---

## **2. Automated Testing with Pytest**

**Purpose:** Ensure endpoints work consistently with repeated runs and CI/CD pipelines.

### **2.1 Setup**

```bash
pip install pytest pytest-asyncio httpx
```

### **2.2 FastAPI Example**

```python
from fastapi.testclient import TestClient
from main import app

client = TestClient(app)

def test_create_post():
    response = client.post("/posts/", json={"title":"Test","content":"Hello","author_id":1})
    assert response.status_code == 201
    assert response.json()["title"] == "Test"

def test_get_posts():
    response = client.get("/posts/")
    assert response.status_code == 200
    assert isinstance(response.json(), list)
```

### **2.3 Django Example**

```python
from django.test import TestCase
from .models import Post

class PostAPITests(TestCase):
    def test_post_creation(self):
        post = Post.objects.create(title="Test", content="Hello", author_id=1)
        self.assertEqual(post.title, "Test")
```

---

## **3. Logging & Error Handling**

### **3.1 Logging**

* Record application events and errors for debugging:

```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

logger.info("Blog API started")
logger.error("An unexpected error occurred")
```

### **3.2 Error Handling**

* Handle exceptions gracefully and return appropriate HTTP responses

**FastAPI Example**

```python
from fastapi import HTTPException

@app.get("/posts/{post_id}")
def get_post(post_id: int):
    post = find_post(post_id)
    if not post:
        raise HTTPException(status_code=404, detail="Post not found")
    return post
```

**Django Example**

```python
from django.http import JsonResponse
from .models import Post

def get_post(request, post_id):
    try:
        post = Post.objects.get(id=post_id)
    except Post.DoesNotExist:
        return JsonResponse({"error": "Post not found"}, status=404)
    return JsonResponse({"title": post.title, "content": post.content})
```

---

## **4. API Documentation**

**Purpose:** Make API self-explanatory for developers and clients.

### **4.1 FastAPI**

* Auto-generates **Swagger UI** at `/docs`
* Add **docstrings** to endpoints for clarity

```python
@app.post("/posts/", response_model=Post)
def create_post(post: Post):
    """
    Create a new blog post.
    - title: string
    - content: string
    """
    return save_post(post)
```

### **4.2 Django (DRF)**

* Install DRF:

```bash
pip install djangorestframework
```

* Use **Browsable API** or **Swagger/OpenAPI** via `drf-yasg` or `drf-spectacular`

---

## **5. Project: Full-Featured Blog/Dashboard API**

### **5.1 Features**

1. User registration & login
2. CRUD operations for posts and comments
3. Dashboard metrics: total posts, active users, comments count
4. Logging for all API requests
5. Robust error handling for invalid inputs and unauthorized actions
6. Automated tests for all endpoints
7. API documentation for developers

### **5.2 Suggested File Structure**

```
blog_dashboard_api/
├─ main.py
├─ models.py
├─ routers/
│   ├─ posts.py
│   └─ users.py
├─ tests/
│   └─ test_posts.py
├─ database.py
├─ requirements.txt
└─ README.md
```

---

## **6. Assignments (Weeks 27–28)**

1. **Postman Manual Testing**

   * Test all CRUD endpoints for posts, comments, users
   * Validate responses, status codes, and authentication

2. **Automated Testing**

   * Write Pytest cases for each endpoint
   * Include edge cases: missing fields, invalid IDs, unauthorized access

3. **Logging Implementation**

   * Log every API request and response
   * Record errors and exceptions

4. **Error Handling**

   * Return meaningful error messages for invalid inputs
   * Use standard HTTP codes (400, 401, 403, 404, 500)

5. **API Documentation**

   * Ensure Swagger UI or DRF schema is fully documented
   * Include examples for each endpoint

6. **Integration**

   * Connect users → posts → comments workflow
   * Verify that metrics and dashboard endpoints reflect real data

---

## **7. Learning Outcomes (Weeks 27–28)**

By the end of this phase, learners will be able to:

* Perform **manual API testing** with Postman
* Implement **automated testing** using Pytest
* Apply **logging and error handling** best practices
* Generate professional **API documentation**
* Deliver a **production-ready Blog/Dashboard API** with robust, maintainable, and well-tested code

---
