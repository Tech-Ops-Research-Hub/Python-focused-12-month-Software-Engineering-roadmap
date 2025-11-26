# **Phase 6: DevOps & Deployment (Weeks 41–46) — Detailed Guide**

This phase equips learners with the skills to **package, deploy, and maintain Python full-stack applications** using modern DevOps practices. The goal is to deliver a **production-ready MVP** accessible online.

---

## **1. GitHub Workflows & CI/CD Basics (Weeks 41–42)**

**Purpose:** Automate testing, building, and deployment to ensure reliable releases.

### **1.1 Workflow Setup**

* Create `.github/workflows/ci.yml` in your repository
* Example: Python project CI

```yaml
name: Python CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: 3.11
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run tests
        run: pytest
```

### **1.2 Key Concepts**

* **Push triggers:** Run workflows automatically on commits
* **Job steps:** Checkout code → setup Python → install → test
* **Badges:** Add workflow status badge to README

**Assignment:** Configure GitHub Actions to automatically run tests on push and PR.

---

## **2. Docker: Containerize Python Apps (Weeks 43–44)**

**Purpose:** Ensure applications run consistently across all environments.

### **2.1 Dockerfile Example (FastAPI)**

```dockerfile
FROM python:3.11-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### **2.2 Docker Commands**

```bash
docker build -t myapp .
docker run -d -p 8000:8000 myapp
```

### **2.3 Docker Compose (Optional)**

```yaml
version: "3.9"
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
      POSTGRES_DB: mydb
```

**Assignment:** Dockerize your full-stack backend with optional database container.

---

## **3. Deploy Apps to Heroku, AWS, or Vercel (Weeks 45–46)**

### **3.1 Deploy FastAPI/Django to Heroku**

1. Install Heroku CLI:

```bash
heroku login
heroku create myapp
```

2. Create `Procfile`:

```
web: uvicorn main:app --host=0.0.0.0 --port=${PORT:-5000}
```

3. Push to Heroku:

```bash
git push heroku main
```

4. Configure environment variables:

```bash
heroku config:set DATABASE_URL=postgres://user:pass@host:port/db
```

### **3.2 Deploy Frontend (React/NextJS)**

* Vercel:

  1. Connect GitHub repo
  2. Configure build command: `npm run build`
  3. Output directory: `build` or `.next`

* AWS (EC2/S3/Amplify) or Render for full-stack apps

**Assignment:** Deploy full-stack project online and verify all API endpoints and frontend pages.

---

## **4. Logging, Monitoring & Environment Variables**

### **4.1 Logging**

```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)
logger.info("App started successfully")
logger.error("Error occurred while processing request")
```

### **4.2 Monitoring**

* Use free tools like **Sentry**, **LogRocket**, or **Prometheus** for error tracking and metrics

### **4.3 Environment Variables**

* Store secrets and configuration safely:

```bash
# .env
DATABASE_URL=postgres://user:pass@host:port/db
SECRET_KEY=mysecret
```

```python
import os
db_url = os.getenv("DATABASE_URL")
```

**Assignment:** Implement logging, environment variables, and monitor app health post-deployment.

---

## **5. Project: Deploy Full-Stack MVP**

### **Features**

1. Backend API (FastAPI/Django)
2. Frontend (HTML/CSS/JS or React/NextJS)
3. Full CRUD functionality for core entities
4. Integrated database (PostgreSQL)
5. Deployment online via Heroku, Vercel, or AWS
6. CI/CD pipeline for automated testing and deployment
7. Logging, monitoring, and secure environment variable usage

### **Suggested Structure**

```
fullstack-mvp/
├─ backend/
│   ├─ main.py
│   ├─ models.py
│   └─ requirements.txt
├─ frontend/
│   ├─ index.html or src/
│   └─ package.json
├─ docker-compose.yml
├─ .github/workflows/ci.yml
├─ .env
└─ README.md
```

---

## **6. Learning Outcomes (Weeks 41–46)**

By the end of this phase, learners will be able to:

* Set up **GitHub workflows** for CI/CD
* **Containerize Python applications** using Docker
* Deploy backend and frontend to **Heroku, AWS, or Vercel**
* Implement **logging, monitoring, and environment variable management**
* Deliver a **production-ready full-stack MVP** accessible online
* Maintain applications with **automated testing and deployment pipelines**

---
