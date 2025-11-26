# **Weeks 23–26: Databases — Detailed Beginner-Friendly Guide**

This phase focuses on **database fundamentals, advanced ORM usage, and building relational database-backed projects**. Learners will use **PostgreSQL** and Python ORMs to integrate data storage into applications, culminating in a **Notes App** project.

---

## **1. SQL & PostgreSQL Basics**

### **1.1 Install PostgreSQL**

* Download from [postgresql.org](https://www.postgresql.org/download/)
* Create a user and database for your project

```sql
-- Create database
CREATE DATABASE notes_app;

-- Create user
CREATE USER notes_user WITH PASSWORD 'securepassword';

-- Grant privileges
GRANT ALL PRIVILEGES ON DATABASE notes_app TO notes_user;
```

### **1.2 Key SQL Concepts**

* **Tables:** store structured data
* **Columns:** define data types (integer, text, timestamp)
* **Primary Key:** unique identifier
* **Foreign Key:** links tables

**Example:**

```sql
CREATE TABLE notes (
    id SERIAL PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    content TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## **2. Python ORM Integration**

**Concept:** Object-Relational Mapping allows Python classes to interact with relational databases seamlessly.

### **2.1 SQLAlchemy (For FastAPI)**

```python
from sqlalchemy import Column, Integer, String, Text, DateTime
from sqlalchemy.ext.declarative import declarative_base
from datetime import datetime

Base = declarative_base()

class Note(Base):
    __tablename__ = "notes"
    id = Column(Integer, primary_key=True, index=True)
    title = Column(String(100), nullable=False)
    content = Column(Text)
    created_at = Column(DateTime, default=datetime.utcnow)
```

* Connect to PostgreSQL:

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "postgresql://notes_user:securepassword@localhost/notes_app"
engine = create_engine(DATABASE_URL)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base.metadata.create_all(bind=engine)
```

---

### **2.2 Django ORM (Alternative)**

```python
# shop/models.py
from django.db import models
from django.contrib.auth.models import User

class Note(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    title = models.CharField(max_length=100)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
```

* Migrations:

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## **3. Relationships & Advanced Queries**

### **3.1 One-to-Many**

* Each user can have multiple notes

```python
class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)
    name = Column(String)
    notes = relationship("Note", back_populates="user")
```

### **3.2 Queries**

```python
# Fetch all notes for a user
session.query(Note).filter(Note.user_id == 1).all()

# Order by creation date descending
session.query(Note).order_by(Note.created_at.desc()).all()
```

---

## **4. Project: Notes App with Relational DB**

### **4.1 Features**

1. User registration & login
2. Create, read, update, delete notes
3. Notes linked to specific users (one-to-many)
4. Optional: search notes by title

### **4.2 Suggested File Structure**

```
notes_app/
├─ main.py          # FastAPI or Django views
├─ models.py        # SQLAlchemy or Django models
├─ schemas.py       # Pydantic models (FastAPI)
├─ database.py      # DB connection
├─ routers/
│   └─ notes.py
└─ requirements.txt
```

---

## **5. Assignments (Weeks 23–26)**

### **Assignment 1: SQL Practice**

* Create tables for users and notes
* Insert sample data
* Perform basic SELECT, UPDATE, DELETE queries

### **Assignment 2: ORM Integration**

* Map Python classes to tables
* Implement CRUD operations via ORM
* Test database interactions

### **Assignment 3: Notes App Features**

* Allow users to create, view, edit, delete notes
* Implement user authentication
* Query notes per user
* Optional: implement search and sorting

### **Assignment 4: Deployment Preparation**

* Configure database connection for deployment
* Test DB integration locally and in Docker

---

## **6. Learning Outcomes (Weeks 23–26)**

By the end of this phase, learners will be able to:

* Understand SQL fundamentals and PostgreSQL setup
* Use Python ORM (SQLAlchemy or Django ORM) to interact with databases
* Model relationships (one-to-many) and write advanced queries
* Build a **Notes App** with relational DB support and user-specific data
* Prepare database-backed applications for production deployment

---
