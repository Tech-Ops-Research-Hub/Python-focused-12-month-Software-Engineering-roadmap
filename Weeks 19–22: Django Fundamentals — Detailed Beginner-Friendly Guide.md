# **Weeks 19–22: Django Fundamentals — Detailed Beginner-Friendly Guide**

This phase introduces **Django**, a high-level Python web framework, focusing on building structured web applications with **ORM, migrations, and user authentication**. The final goal is to build an **E-commerce Backend**.

---

## **1. Setting Up Django**

### **1.1 Install Django**

```bash
pip install django
```

### **1.2 Create Project & App**

```bash
django-admin startproject ecommerce
cd ecommerce
python manage.py startapp shop
```

**Structure:**

```
ecommerce/
├─ ecommerce/      # Project settings
│   ├─ settings.py
│   ├─ urls.py
├─ shop/           # App for products, orders, users
│   ├─ models.py
│   ├─ views.py
│   ├─ urls.py
└─ manage.py
```

---

## **2. ORM & Migrations**

**Concept:** Django ORM maps Python classes to database tables. Migrations keep database schema synchronized with models.

### **2.1 Defining Models**

```python
from django.db import models
from django.contrib.auth.models import User

class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=8, decimal_places=2)
    stock = models.PositiveIntegerField()
    description = models.TextField()

class Order(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    quantity = models.PositiveIntegerField()
    created_at = models.DateTimeField(auto_now_add=True)
```

### **2.2 Running Migrations**

```bash
python manage.py makemigrations
python manage.py migrate
```

* `makemigrations` → creates migration files from model changes
* `migrate` → applies migrations to database

---

## **3. User Authentication & Authorization**

### **3.1 Built-in User Model**

* Django includes authentication out-of-the-box: `User` model, login, logout, registration

### **3.2 Creating Superuser**

```bash
python manage.py createsuperuser
```

* Allows admin access to manage users and products

### **3.3 Protecting Views**

```python
from django.contrib.auth.decorators import login_required

@login_required
def order_list(request):
    # Only logged-in users can access orders
    pass
```

---

## **4. Views & URL Routing**

### **4.1 URL Patterns**

```python
from django.urls import path
from . import views

urlpatterns = [
    path('products/', views.product_list, name='product_list'),
    path('orders/', views.order_list, name='order_list'),
]
```

### **4.2 Views Example**

```python
from django.http import JsonResponse
from .models import Product

def product_list(request):
    products = list(Product.objects.values())
    return JsonResponse(products, safe=False)
```

* Returns JSON data suitable for API consumption

---

## **5. Project: E-commerce Backend**

### **5.1 Features**

1. Product CRUD (Create, Read, Update, Delete)
2. User registration and login
3. Order management (create, view orders)
4. Data validation using Django models
5. Optional: Admin interface customization

### **5.2 Suggested File Structure**

```
ecommerce/
├─ ecommerce/
│   ├─ settings.py
│   ├─ urls.py
├─ shop/
│   ├─ models.py
│   ├─ views.py
│   ├─ urls.py
│   ├─ serializers.py (optional for DRF integration)
└─ manage.py
```

---

## **6. Assignments (Weeks 19–22)**

### **Assignment 1: Project Setup**

* Initialize Django project & app
* Configure database (SQLite for beginners)
* Create superuser

### **Assignment 2: Models & Migrations**

* Create Product and Order models
* Run migrations
* Verify tables in database

### **Assignment 3: Authentication**

* Implement user registration and login
* Protect order endpoints using `login_required`
* Test access control for authenticated vs non-authenticated users

### **Assignment 4: API Endpoints**

* Build product endpoints: list, create, update, delete
* Build order endpoints: create order, list orders for logged-in user
* Test endpoints using **Postman** or **HTTPie**

### **Assignment 5: Optional Enhancements**

* Implement product search/filtering
* Add user profile model
* Add order history endpoint for users

---

## **7. Learning Outcomes (Weeks 19–22)**

By the end of this phase, learners will be able to:

* Set up Django projects and apps properly
* Use Django ORM and migrations to manage databases
* Implement authentication and protect endpoints
* Build CRUD operations for products and orders
* Deliver a functional **E-commerce Backend** ready for API consumption

---
