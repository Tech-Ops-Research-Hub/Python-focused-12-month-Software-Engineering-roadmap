# **Weeks 27–28: Deployment & CI/CD — Detailed Beginner-Friendly Guide**

This phase focuses on **making your Python backend projects production-ready**, covering **Docker, GitHub Actions for CI/CD, and cloud deployment**.

---

## **1. Docker for Python Applications**

**Concept:** Docker packages applications and dependencies into containers, ensuring **consistent environments** across machines.

### **1.1 Install Docker**

* Download and install Docker Desktop from [docker.com](https://www.docker.com/get-started)

### **1.2 Dockerfile Example (FastAPI Project)**

```dockerfile
# Use official Python image
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Copy requirements
COPY requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy project files
COPY . .

# Run FastAPI server
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### **1.3 Build & Run Container**

```bash
docker build -t blog-api .
docker run -d -p 8000:8000 blog-api
```

* Visit `http://localhost:8000` to verify

---

### **1.4 Docker Compose (Optional for Multi-Service Projects)**

```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "8000:8000"
    depends_on:
      - db
  db:
    image: postgres:15
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: blog_db
    ports:
      - "5432:5432"
```

---

## **2. GitHub Actions (CI/CD)**

**Concept:** Automatically test, build, and deploy your projects on every commit.

### **2.1 Basic Workflow**

* Create `.github/workflows/ci.yml`

```yaml
name: Python CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run tests
        run: pytest
```

* **What it does:** On every push/PR to `main`, it checks out the code, installs dependencies, and runs tests.

---

## **3. Cloud Deployment**

### **3.1 Deploy FastAPI on Render**

1. Create a free account on [Render](https://render.com/)
2. Connect GitHub repository
3. Select “Web Service” → `Python` → `Start Command: uvicorn main:app --host 0.0.0.0 --port 10000`
4. Render builds and deploys automatically

### **3.2 Deploy Django on Heroku (Optional)**

1. Install Heroku CLI

```bash
heroku login
heroku create ecommerce-backend
git push heroku main
```

2. Add `Procfile`:

```
web: gunicorn ecommerce.wsgi --log-file -
```

3. Configure environment variables (DATABASE_URL, SECRET_KEY, etc.)

---

## **4. Assignments (Weeks 27–28)**

### **Assignment 1: Dockerize Project**

* Create Dockerfile for FastAPI or Django project
* Build and run container locally
* Verify project works inside container

### **Assignment 2: Docker Compose**

* If using DB, set up `docker-compose.yml` with web and database
* Test connectivity between services

### **Assignment 3: CI/CD with GitHub Actions**

* Configure workflow to install dependencies and run tests on push
* Add workflow badge to README

### **Assignment 4: Cloud Deployment**

* Deploy project to Render (FastAPI) or Heroku (Django)
* Test endpoints live on the web
* Optional: Add automated deployment via GitHub Actions

---

## **5. Learning Outcomes (Weeks 27–28)**

By the end of this phase, learners will be able to:

* Containerize Python projects with Docker for consistent environments
* Use Docker Compose for multi-service applications (backend + database)
* Set up GitHub Actions for continuous integration and testing
* Deploy FastAPI or Django projects to cloud platforms
* Deliver production-ready backend services with automated CI/CD pipelines

---
