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

[Back to Index](index.md)
