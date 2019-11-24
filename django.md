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

4. run `python manage.py collectstatic`

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

## Adding a Media Folder and Uploading

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

## Modifying the Admin Templates

### Sample base_site.html

    ```html+jinja
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

### Sample admin.css

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

## Modify Admin List Display for Model

Create an `admin.ModelAdmin` derived class to customize list displays and register with the model class in admin.py for app.

```python
class ListingAdmin(admin.ModelAdmin):
    list_display = ('id', 'title', 'is_published', 'price', 'list_date', 'realtor')
    list_display_links = ('id', 'title')
    list_filter = ('realtor', )
    list_editable = ('is_published', )
    search_fields = ('title', 'description', 'address', 'city', 'state', 'zipcode', 'price')
    list_per_page = 25

admin.site.register(Listing, ListingAdmin)
```

## Querying Tables from a Page Request

The following view function show how to chain filters to a query to reduce elements in the final result.

```python
def search(request):

    queryset_list = Listing.objects.order_by("-list_date")

    # Only show published listings
    queryset_list = queryset_list.filter(is_published=True)

    # Keyword field filter
    if "keywords" in request.GET:
        keywords = request.GET["keywords"]
        if keywords:
            queryset_list = queryset_list.filter(description__icontains=keywords)

    # City field filter
    if "city" in request.GET:
        city = request.GET["city"]
        if city:
            queryset_list = queryset_list.filter(city__iexact=city)

    # state field filter
    if "state" in request.GET:
        state = request.GET["state"]
        if state:
            queryset_list = queryset_list.filter(state__iexact=state)

    # bedrooms field filter
    if "bedrooms" in request.GET:
        bedrooms = request.GET["bedrooms"]
        if bedrooms:
            queryset_list = queryset_list.filter(bedrooms__lte=bedrooms)

    # price field filter
    if "price" in request.GET:
        price = request.GET["price"]
        if price:
            queryset_list = queryset_list.filter(price__lte=price)

    context = {
        "bedroom_choices": bedroom_choices,
        "price_choices": price_choices,
        "state_choices": state_choices,
        "listings": queryset_list,
    }
    return render(request, "listings/search.html", context)
```

## Populate form values with values from original request

In the context pass the values received from request.GET

```python
    context = {
        "bedroom_choices": bedroom_choices,
        "price_choices": price_choices,
        "state_choices": state_choices,
        "listings": queryset_list,
        'values': request.GET
    }
```

The for the fields either pass in the value for that field (for input fields) or test that the current item is equal to the original request value and set it as selected (option lists, radio buttons, check boxes)

    ```
    <div class="col-md-4 mb-3">
        <label class="sr-only">City</label>
        <input type="text" name="city" class="form-control" placeholder="City"  value="{{ values.city }}">
    </div>

    <div class="col-md-4 mb-3">
        <label class="sr-only">State</label>
        <select name="state" class="form-control">
        <option selected="true" disabled="disabled">State (All)</option>
        {% for key, value in state_choices.items %}
        <option value="{{key}}" {% if values.state == key %}selected="true"{% endif %}>{{value}}</option>
        {% endfor %}
        </select>
    </div>
    ```

## Dismissable Flash Errors Message Partial

Add the following to the bottom of the project `settings.py`

```python
# Messages
from django.contrib.messages import constants as messages
MESSAGE_TAGS = {
    messages.ERROR: 'danger',
}
```

The create a partial template that contains the following

    ```
    {% if messages %}
    {% for message in messages %}
        <div id="message" class="container">
          <div class="alert alert-{{message.tags}} alert-dismissable text-center" role="alert">
            <button type='button' class="close" data-dismiss="alert"><span aria-hidden="true">&times;</span></button>
            <strong>
              {% if message.level == DEFAULT_MESSAGE_LEVELS.ERROR %}
              Error
              {% else %}
                {{message.tags|title}}
              {% endif %}
            </strong>
            {{message}}
          </div>
        </div>
    {% endfor %}
    {% endif %}
    ```

## Sample Dockerfile

```
FROM python:3.6

ENV PYTHONUNBUFFERED 1
RUN mkdir /code
WORKDIR /code
COPY requirements.txt /code/
RUN pip install -r requirements
COPY . /code/
```

[Back to Index](index.md)
