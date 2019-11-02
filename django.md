# Django

## Creating a new Django Project

1. Create a folder for the project
2. Create a virtual environment: `python3 -m venv venv`
3. Start the virtual environment `source venv/bin/activate`
4. Install Django: `pip install django`
5. Start a new project: `django-admin startproject <project_name> .`

## Run the development server

Run `python manage.py runserver`

## Adding an app to the project

Inside the project folder with the virtual environment activated:

1. Run `python manage.py startapp <app_name>
2. Add the app the the list of installed apps:

```python
INSTALLED_APPS = [
    '<app_name>.apps.<AppName>Config',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

3. Create a new urls.py file in the app folder with the following contents:

```python
from django.urls import path

from . import views


urlpatterns = [
    path("", views.index, name="index"),
    path("about", views.about, name="about"),
]
```

4. In the project urls.py add a path to the app urls.py:
(Remember to import include)

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("", include("<app_name>.urls")),
    path("admin/", admin.site.urls),
]
```

5. Add view functions to the apps views.py file

```python
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.

def index(request):
    return render(request, 'pages/index.html')

def about(request):
    return render(request, 'pages/about.html')
```

## Dealing with Static Files

1. In your main project folder create a folder called 'static'
2. Copy your static assets into the folder. You can use subdirectories if necessary
3. In settings.py add the following:

```python
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, '<project_name>/static')
]
```

4. run `python manage.py collectstatic'

This will create a static folder in the root of the project.

## Models and Migrations

### Sample docker-compose.yml for Database and Admin Utility

```
version: '3.1'

services:
  db:
    image: postgres
    restart: always
    ports:
      - 5432:5432
    environment:
      POSTGRES_PASSWORD: password

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080

```

### Changes to settings.py to support database

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'btredb',
        'USER': 'postgres',
        'PASSWORD': 'password',
        'HOST': 'localhost'

    }
}
```

Run `python manage.py migrate`
The database should be located under the public schema.

### Creating Models

#### Sample Model File

```python
from django.db import models
from datetime import datetime
# Create your models here.

class Realtor(models.Model):
    name = models.CharField(max_length=200)
    photo = models.ImageField(upload_to='photos/%Y/%m/%d/')
    description = models.TextField(blank=True)
    phone = models.CharField(max_length=20)
    email = models.CharField(max_length=50)
    is_mvp = models.BooleanField(default=False)
    hire_date = models.DateTimeField(default=datetime.now, blank=True)

    def __str__(self):
        return self.name
```

#### Adding Models to the Database

Run the following:
`python manage.py makemigrations`
`python manage.py migrate`

#### Adding Models to The Admin Site

1. Create a superuser: `python manage.py createsuperuser`
2. Update the admin.py for the app to add the model

```python
from django.contrib import admin
from .models import Realtor

# Register your models here.

admin.site.register(Realtor)
```

3. Log into the admin area `http://localhost/admin` and log in
4. The model should be visible

### Adding a Media Folder and Uploading

1. Add the following to settings.py

```python
# Media Folder Settings

MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

2. Add the following to urls.py

```python
...
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path("", include("pages.urls")),
    path("listings/", include("listings.urls")),
    path("admin/", admin.site.urls),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

### Modifying the Admin Templates

#### Sample base_site.html

```
{% extends 'admin/base.html' %}
{% load static %}

{% block branding %}
<h1 id="head">
  <img src="{% static 'img/logo.png' %}" alt="BT Real Estate" class="brand_img" height="50" width="80"> Admin Area
</h1>
{% endblock %}
{% block extrastyle %}
  <link rel="stylesheet" href="{% static 'css/admin.css' %}">
{% endblock %}
```

#### Sample admin.css

```
#header {
  height: 80px;
  background: #10284e;
  color: #ffffff;
}

#branding h1 {
  color: #ffffff;
}

a:link,
a:visited {
  color: #10284e;

}

div.breadcrumbs {
  background-color: #30caa0;
  color: #10284e;
}

div.breadcrumbs a {
  color: #333;
}

.module h2, 
.module caption, 
.inline-group h2 {
  background-color: #30caa0; 
}

.button,
input[type=submit],
input[type=button],
.submit=row input.
a.button {
  background: #10284e;
  color: #ffffff;
}
```

[Back to Index](index.md)
