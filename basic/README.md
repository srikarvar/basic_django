# Getting Started with Django

This guide is designed for beginners who are starting out with Django for the first time. It will walk you through the process of setting up a basic Django app, creating a simple model, adding a home page, managing todos, and accessing the admin panel.

## Prerequisites

- Python (3.6 or higher)
- Pip (Python package installer)

## Setup

1. **Clone the Repository:**

    ```bash
    git clone https://github.com/your-username/your-django-app.git
    cd your-django-app
    ```

2. **Create and Activate a Virtual Environment:**

    ```bash
    python -m venv venv
    source venv/bin/activate
    ```

3. **Install Django:**

    ```bash
    pip install django
    ```

4. **Run Migrations:**

    ```bash
    python manage.py migrate
    ```

## Creating a Basic App

1. **Create a New Django App:**

    ```bash
    python manage.py startapp myapp
    ```

2. **Define a Simple Model:**

    In `myapp/models.py`, define the following model:

    ```python
    from django.db import models
   
    class TodoItem(models.Model):
        title = models.CharField(max_length=200)
        completed = models.BooleanField(default=False)
   
    ```

3. **Apply Model Changes:**

    ```bash
    python manage.py makemigrations myapp
    python manage.py migrate
    ```

## Home Page and Todos

1. **Define Views:**

    In `myapp/views.py`, define the following views:

    ```python
    from django.shortcuts import render
    from .models import TodoItem
   
    def home(request):
    return render(request, "home.html")


    def todos(request):
        items = TodoItem.objects.all()
        return render(request, "todos.html", {"todos": items})
    ```

2. **Create a Template for the Home Page:**
    Also keep in mind to create base.html:

## Base Template (base.html)

Use the following `base.html` template as the foundation for your app's templates:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}Your Website Title{% endblock %}</title>
    <!-- Include Bootstrap CSS link here -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        /* Custom style for title color */
        .navbar-title {
            color: #333; /* Change to your desired color */
        }
    </style>
</head>
<body>

<nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
        <a class="navbar-brand" href="#">
            <img src="your-logo.png" alt="Logo" width="30" height="30" class="d-inline-block align-top">
            <span class="navbar-title">{% block navbar_title %}Your Brand{% endblock %}</span>
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
                aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav">
                <li class="nav-item active">
                    <a class="nav-link" href="#">Home</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">About</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Services</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Contact</a>
                </li>
            </ul>
        </div>
    </div>
</nav>

<div class="container mt-4">
    {% block content %}
    {% endblock %}
</div>

<!-- Include Bootstrap JS and jQuery scripts here -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

    Create a template at `myapp/templates/myapp/todos.html` 
    with the following content:

    ```html
    {% extends "base.html" %}

{% block title %}Home{% endblock %}

{% block content %}
<h1>Todo List</h1>
<ul>
    {% for todo in todos %}
        <li>{{ todo.title }} - {% if todo.completed %}Completed{% else %}Pending{% endif %}</li>
    {% endfor %}
</ul>
{% endblock %}

    ```

3. **Configure URLs:**

    In `myapp/urls.py`, configure the URLs as follows:

    ```python
    from django.urls import path
    from . import views
   
    urlpatterns = [
    path('', views.home, name='home'),
    path('todos/', views.todos, name='Todos'),
    ]
    ```

## Admin Panel and Superuser

1. **Create a Superuser:**

    ```bash
    python manage.py createsuperuser
    ```

2. **Access the Admin Panel:**

    Access the admin panel at `http://localhost:8000/admin/` and log in with the superuser credentials.

3. **Register the `Todo` Model:**

    In `myapp/admin.py`, register the `Todo` model:

    ```python
    from django.contrib import admin
    from .models import TodoItem
   
    admin.site.register(TodoItem)
    ```

## Running the App

1. **Run the Development Server:**

    ```bash
    python manage.py runserver
    ```

2. **Access the App:**

    Access the app at `http://localhost:8000/`, `http://localhost:8000/home`, `http://localhost:8000/todos`


## Contributing

Feel free to contribute to this project by submitting pull requests or reporting issues.

Happy coding!
