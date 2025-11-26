# **PHASE 0 — Orientation & Setup (Week 0)**

**Goal:** Build a clean, standardized development environment and establish the foundational workflow required for all future engineering tasks.

---

# **1. Development Environment Setup**

## **1.1 Install Python (Latest Stable CPython Release)**

A correct Python setup determines interpreter stability and dependency isolation throughout the program.

**Requirements**
– Install the official CPython release from python.org.
– Add Python to PATH during installation.
– Confirm installation:

```
python --version
pip --version
```

**Baseline Packages to Install Immediately**
These anchor future lessons:

```
pip install requests fastapi[standard] pydantic pytest black ruff
```

**Configuration Standards**
– Set Python as the default interpreter in VS Code.
– Use Black for opinionated formatting to prevent style drift.
– Use Ruff for fast linting across the entire project.

---

## **1.2 Install Visual Studio Code (VS Code)**

VS Code will act as the primary coding environment.

**Required Extensions**
– Python
– Black Formatter
– Ruff
– GitLens
– Docker
– GitHub Pull Requests & Issues

**Core Configurations**
Add these to VS Code settings:

```
"editor.formatOnSave": true,
"python.formatting.provider": "black",
"python.linting.enabled": true,
"ruff.lint.args": ["--fix"]
```

**Outcome**
Every saved file immediately conforms to a strict, industry-standard style.

---

## **1.3 Install Git & Configure Identity**

Version control is introduced at Phase 0 to prevent early undisciplined habits.

**Commands**

```
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
git config --global core.autocrlf false
```

**Rationale**
– Ensures traceable commit history.
– Prevents CRLF conflicts across operating systems.

---

## **1.4 Install Docker**

Docker allows you to containerize the backend applications you will build later.

**Verification**

```
docker --version
docker run hello-world
```

**Minimum Concepts Required in Week 0**
– Image
– Container
– Dockerfile
– docker build
– docker run

Nothing more. Orchestration belongs to later phases.

---

# **2. GitHub Setup & Engineering Workflow**

## **2.1 Create GitHub Account**

– Use a professional username.
– Enable 2FA.
– Add SSH key to GitHub:

```
ssh-keygen -t ed25519
```

Add the public key to GitHub Settings → SSH and GPG keys.

---

## **2.2 Create the First Repository (“se-learning-journey”)**

This repo will contain:
– Week 0 setup
– Notes
– Practice scripts
– Early exercises

Later projects will live in their own repositories, but Week 0 uses a single sandbox.

---

## **2.3 Adopt the Standard Development Workflow**

### **Branching Model**

– `main` = finished work
– Every task happens inside a feature branch
Example:

```
git checkout -b setup-environment
```

### **Commit Discipline**

Message prefixes:
– `feat:` new feature
– `fix:` bug fix
– `refactor:` structure changes
– `docs:` documentation
– `chore:` housekeeping

Example commit messages:

```
feat: initialize python virtual environment
docs: add development environment notes
refactor: reorganize project folder structure
```

### **Pull Request Routine (Even for Solo Learners)**

– Open PR with clear title and summary.
– Review your own diff.
– Merge when satisfied.
This builds habits for team environments.

---

# **3. Virtual Environments, Dependency Control & Project Structure**

## **3.1 Create and Use Virtual Environments**

Required for every project—no exceptions.

**Commands**

```
python -m venv venv
source venv/bin/activate   # macOS/Linux
venv\Scripts\activate      # Windows
```

**Rules**
– Install packages only inside the venv.
– Track exact dependencies:

```
pip freeze > requirements.txt
```

---

## **3.2 Project Structure Template**

Every Python project starts with this minimal structure:

```
project_name/
    venv/
    app/
        __init__.py
        main.py
    tests/
        test_main.py
    requirements.txt
    README.md
```

**Purpose of Each Component**
– `app/` contains source code only.
– `tests/` ensures test-driven thinking from the start.
– `__init__.py` makes the directory importable.
– `README.md` clarifies purpose and usage.

This structure remains consistent across all subsequent phases, building strong engineering habits.

---

# **4. Portfolio Project Planning**

The curriculum expects long-term output from Day 1. Planning starts in Week 0 to align learning with execution.

## **4.1 Select Three Core Project Directions**

### **Category A: Python Utility / CLI Project**

Scope: simple, functional, demonstrating clean Python fundamentals.
Examples:
– File organizer
– Expense parser
– PDF manipulation tool
– Web scraper

### **Category B: Backend API (FastAPI or Django)**

Scope: CRUD operations, validation, database integration.
Examples:
– Notes API
– Blog API
– Inventory system API
– Authentication microservice

### **Category C: Full Product (API + Database + Frontend + Deployment)**

Scope: real-world architecture.
Examples:
– Mini fintech service (loan/credit scoring module)
– E-learning microplatform
– Task automation service
– Small SaaS tool

---

## **4.2 Define the Problem Statement for Each Project**

Each selected project must include:
– Problem
– Target user
– Functional scope
– Non-functional constraints
– Minimum features

Example template:

```
# Project Name

## Problem
State the real problem you want to solve.

## Target Users
Define who is affected.

## Core Features
- Feature 1
- Feature 2
- Feature 3

## Non-Functional Requirements
- Performance
- Error handling
- Logging

## Tech Stack
Python + FastAPI / Django
PostgreSQL
Docker
```

Stating this clearly prevents scope creep and teaches professional requirements analysis.

---

# **5. End-of-Week Checklist for the Learner**

**You must complete all the following items before starting Phase 1:**

### Environment

[ ] Python installed and verified
[ ] VS Code fully configured
[ ] Git installed and configured
[ ] Docker installed and running

### GitHub & Workflow

[ ] SSH keys connected
[ ] “se-learning-journey” repo created
[ ] First feature branch created
[ ] PR created and merged
[ ] Commit discipline applied

### Python Project Setup

[ ] Virtual environment created
[ ] requirements.txt generated
[ ] Standard project structure established

### Portfolio Planning

[ ] One utility project chosen
[ ] One backend project chosen
[ ] One full-stack product defined
[ ] Problem statements completed and documented

---

