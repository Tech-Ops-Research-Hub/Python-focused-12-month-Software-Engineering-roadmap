# **Phase 7: Capstone Project (Weeks 47–52) — Detailed Guide**

This is the **final phase**, where learners consolidate all skills from previous phases to **build a professional, portfolio-ready full-stack application**. The emphasis is on **real-world application, deployment, and showcase readiness**.

---

## **1. Project Selection**

**Purpose:** Apply everything learned to a complete system.

### **1.1 Choose a Real-World Domain**

* **Fintech App:** Expense tracker, BNPL, loan management
* **E-Learning Platform:** Course listing, enrollment, progress tracking
* **Social Platform:** Posts, comments, likes, user feeds

### **1.2 Define MVP Scope**

* Minimum features needed to demonstrate full-stack integration
* Backend CRUD, database models, frontend interface, and authentication

**Assignment:** Write a project brief with objectives, features, and milestones.

---

## **2. Backend Development (Weeks 47–50)**

**Purpose:** Implement robust server-side functionality.

### **2.1 FastAPI/Django Setup**

* Define models for core entities
* Implement CRUD operations
* Integrate relational database (PostgreSQL)
* Apply authentication (JWT for FastAPI, Django Auth or DRF Tokens)

**Example: FastAPI Model**

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.orm import relationship
from database import Base

class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)
    username = Column(String, unique=True, index=True)
    password = Column(String)
    posts = relationship("Post", back_populates="author")

class Post(Base):
    __tablename__ = "posts"
    id = Column(Integer, primary_key=True)
    title = Column(String)
    content = Column(String)
    author_id = Column(Integer, ForeignKey("users.id"))
    author = relationship("User", back_populates="posts")
```

### **2.2 Assignment**

* Implement all backend endpoints with validation
* Secure sensitive routes with authentication
* Test endpoints using Postman and Pytest

---

## **3. Frontend Integration (Weeks 51)**

**Purpose:** Create an interface that interacts with the backend.

### **3.1 Minimal Frontend**

* Vanilla JS or template-based HTML/CSS
* Fetch API data and render dynamically

### **3.2 Optional React Integration**

```javascript
useEffect(() => {
  fetch("https://api.myapp.com/posts")
    .then(res => res.json())
    .then(data => setPosts(data))
    .catch(err => console.error(err));
}, []);
```

### **3.3 Assignment**

* Connect frontend to backend endpoints
* Implement authentication flows (login/register)
* Display dynamic data: posts, users, transactions, or courses

---

## **4. Advanced Features**

* **Authentication:** JWT, session cookies, or OAuth
* **Database Relations:** Users → Posts → Comments
* **Optional Real-Time Features:** WebSockets or polling for notifications/updates
* **Logging & Monitoring:** Track errors, API requests, and user activity

---

## **5. Testing, Debugging, Deployment (Weeks 52)**

### **5.1 Testing**

* Automated tests for all backend endpoints (Pytest or Django TestCase)
* Frontend test flows: form validation, API fetch, error handling

### **5.2 Debugging**

* Use logging, error messages, browser dev tools, and Postman

### **5.3 Deployment**

* Dockerize full-stack app
* Deploy backend: Heroku, AWS, or Render
* Deploy frontend: Vercel, Netlify, or integrated in same deployment
* Set environment variables and database credentials securely

---

## **6. Project: Cloud-Deployed Portfolio-Ready Full-Stack App**

### **6.1 Features**

1. Backend CRUD with authentication
2. Frontend integration displaying real data
3. Database relations
4. Optional real-time features (chat, notifications)
5. Automated testing
6. Logging and monitoring
7. Cloud deployment with CI/CD pipeline

### **6.2 Suggested Structure**

```
capstone-project/
├─ backend/
│   ├─ main.py
│   ├─ models.py
│   ├─ routers/
│   └─ tests/
├─ frontend/
│   ├─ index.html or src/
│   └─ components/
├─ docker-compose.yml
├─ .env
├─ .github/workflows/ci.yml
└─ README.md
```

---

## **7. Assignments & Milestones**

1. **Week 47–48:** Finalize backend models, endpoints, and database integration
2. **Week 49:** Implement authentication and protected routes
3. **Week 50:** Connect frontend to backend and implement dynamic UI
4. **Week 51:** Optional real-time features and enhancements
5. **Week 52:** Full testing, debugging, Dockerization, deployment, and README documentation

---

## **8. Learning Outcomes (Weeks 47–52)**

By the end of this phase, learners will be able to:

* Design and implement a **real-world full-stack application**
* Integrate backend APIs with frontend interfaces
* Apply **authentication, relational databases, and optional real-time features**
* Conduct thorough **testing and debugging**
* Deploy cloud-ready applications with **environment management and logging**
* Deliver a **portfolio-ready MVP** that demonstrates **industry-level capabilities**

---
