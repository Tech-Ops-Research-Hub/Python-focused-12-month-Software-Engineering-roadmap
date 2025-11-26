# **Weeks 23–26: Django Advanced & REST API with DRF — Detailed Beginner-Friendly Guide**

This phase focuses on building a **full REST API** for your e-commerce project using **Django REST Framework (DRF)**, adding advanced features like serialization, permissions, and filtering.

---

## **1. Setting Up DRF**

### **1.1 Install Django REST Framework**

```bash
pip install djangorestframework
```

### **1.2 Add to Installed Apps**

```python
# ecommerce/settings.py
INSTALLED_APPS = [
    ...
    'rest_framework',
    'shop',
]
```

---

## **2. Serializers**

**Concept:** Convert Django models into JSON format for API responses and validate input data.

### **2.1 Create Serializers**

```python
from rest_framework import serializers
from .models import Product, Order

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ['id', 'name', 'price', 'stock', 'description']

class OrderSerializer(serializers.ModelSerializer):
    class Meta:
        model = Order
        fields = ['id', 'user', 'product', 'quantity', 'created_at']
```

---

## **3. API Views**

### **3.1 Using DRF ViewSets**

```python
from rest_framework import viewsets
from .models import Product, Order
from .serializers import ProductSerializer, OrderSerializer
from rest_framework.permissions import IsAuthenticated

class ProductViewSet(viewsets.ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

class OrderViewSet(viewsets.ModelViewSet):
    queryset = Order.objects.all()
    serializer_class = OrderSerializer
    permission_classes = [IsAuthenticated]  # Only logged-in users
```

---

### **3.2 Routing with DRF Routers**

```python
from rest_framework.routers import DefaultRouter
from django.urls import path, include
from .views import ProductViewSet, OrderViewSet

router = DefaultRouter()
router.register(r'products', ProductViewSet)
router.register(r'orders', OrderViewSet)

urlpatterns = [
    path('', include(router.urls)),
]
```

* Automatically creates endpoints for **list, create, retrieve, update, delete**

---

## **4. Filtering, Searching, and Pagination**

### **4.1 Filtering by Fields**

```python
from django_filters.rest_framework import DjangoFilterBackend

class ProductViewSet(viewsets.ModelViewSet):
    ...
    filter_backends = [DjangoFilterBackend]
    filterset_fields = ['price', 'stock']
```

### **4.2 Searching**

```python
from rest_framework import filters

class ProductViewSet(viewsets.ModelViewSet):
    ...
    filter_backends = [filters.SearchFilter]
    search_fields = ['name', 'description']
```

### **4.3 Pagination**

```python
# ecommerce/settings.py
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10
}
```

---

## **5. Permissions & Authentication**

### **5.1 Built-in Permissions**

* `IsAuthenticated`: Only logged-in users
* `IsAdminUser`: Only admin users
* `AllowAny`: Public access

### **5.2 Example: Only Admins Can Modify Products**

```python
from rest_framework.permissions import IsAdminUser

class ProductViewSet(viewsets.ModelViewSet):
    ...
    permission_classes = [IsAdminUser]
```

---

## **6. Project: Full E-commerce REST API**

### **6.1 Features**

1. CRUD operations for **products**
2. CRUD operations for **orders**
3. **User authentication** and access control
4. Search, filter, and pagination for products
5. Optional: order history per user

### **6.2 File Structure**

```
ecommerce/
├─ ecommerce/
│   ├─ settings.py
│   ├─ urls.py
├─ shop/
│   ├─ models.py
│   ├─ serializers.py
│   ├─ views.py
│   ├─ urls.py
└─ manage.py
```

---

## **7. Assignments (Weeks 23–26)**

### **Assignment 1: DRF Setup**

* Install DRF
* Configure settings and apps
* Test `/api/` endpoint returning JSON

### **Assignment 2: Serializers & ViewSets**

* Create `ProductSerializer` and `OrderSerializer`
* Implement CRUD API endpoints using `ModelViewSet`
* Test endpoints with **Postman** or **Swagger UI**

### **Assignment 3: Filtering & Searching**

* Add field filtering (price, stock)
* Add search by product name or description
* Implement pagination for product list

### **Assignment 4: Permissions**

* Ensure only **authenticated users** can create orders
* Restrict product modifications to **admin users**
* Test access restrictions with multiple users

### **Assignment 5: API Documentation**

* Use DRF browsable API or **Swagger UI**
* Document endpoints, fields, and sample requests/responses

---

## **8. Learning Outcomes (Weeks 23–26)**

By the end of this phase, learners will be able to:

* Build fully functional REST APIs using Django REST Framework
* Serialize and validate data efficiently
* Apply authentication and permissions to secure endpoints
* Implement search, filtering, and pagination for scalable APIs
* Deliver a **professional e-commerce backend** ready for frontend integration

---
