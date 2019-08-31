# Django

## Installation and Initial Setup

1. Create a folder for the project and change into it
2. Create a virtual environment and activate `python3 -m venv venv && source venv/bin/activate`
3. Initialize the git repo `git init`
4. Create the .gitignore file (from [gitinore.io](http://gitignore.io))
5. Install django `pip install django`
6. Add and commit files `git add . && git commit -m "Initial commit."`
7. Create github/gitea repo and push initial commit to it
  `git remote add origin <remote_url> && git push -u origin master`

## Adding an app
1. Run `python manage.py startapp <app_name>`
2. Add the new app to settings.py INSTALLED_APPS ex.
`app_name.apps.App_nameConfig`

## Workflow for adding routes to an app

1. Create a `urls.py`  in the app folder with the following for example:
  ```python
  from django.urls import path
  from . import views
  ```
2. Create a path entry in the main urls.py to the app's urls.py
```python
urlpatterns = [
    path('', include('pages.urls')),
    path('admin/', admin.site.urls),
]
```
3. Add a urlpatterns list
```python
urlpatterns = [
    path('', views.index, name='index')
]
```
4. Create a view function in views.py for example:
```python
def index(request):
    return HttpResponse('<h1>Hello World</h1>') 
```
5. Repeat steps 3 and 4 for each url to add to the app

## Templates and Layouts

### Adding templates

1. Update the TEMPLATES DIRS key in settings.py
`'DIRS': [os.path.join(BASE_DIR, 'templates')],`
2. Create a folder on the root call `templates` along with a subfolder for each app
3. Create html file for each view
4. In the app's view, call `return render(request, '<template_file_name>')

### Base Layouts


## Static Files and Paths

### Preparing Static Files

1. Add the following to settings.py:
```python
STATIC_ROOT=os.path.join(BASE_DIR, 'static')
STATIC_URL='/static/'
STATICFILES_DIRS=[
  os.path.join(BASE_DIR, '<projectname>/static')
]
```

### Preparing Media Files
* In settings.py add :
```python
# Media Folder Settings
MEDIA_ROOT=os.path.join(BASE_DIR, 'media')
MEDIA_URL='/media/'
```
* In urls.py modify the urlpatterns to append the following:
`+ static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)`

2. Run `python manage.py collectstatic' during development.  During deployment this should be part of the deployment process.

### Adjusting templates


### Partials
1. Create a folder under templates called partials
2. Cut repeated portions that don't need to be in the base.html and place them in their own file named _<partial_name>.html
3. Add to the original file using `{% include 'partial/_<partial_name>.html' %}

## Linking

1. For internal links in a template use `{% url '<template_name>.html' %}`

## Models

### Setting up a Database

* Install a datanase server using the package manager or docker
* create a database with correct permissions
* Adjust the DATABASES dictionary in `settings.py` for example:
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'btredb',
        'USER': 'postgres',
        'PASSWORD': 'postgres',
        'HOST': 'localhost'
    }
}
```
* Run `python manage.py migrate` to create tables

### Define the Model Field Schemas

Can be done using a text / markdown file or tool

After creating the fields structure, convert it to a model class, for example:
```python
class Listing(models.Model):
    realtor = models.ForeignKey(Realtor, on_delete=models.DO_NOTHING)
    title = models.CharField(max_length=200)
    address = models.CharField(max_length=200)
    city = models.CharField(max_length=100)
    state = models.CharField(max_length=100)
    zipcode = models.CharField(max_length=20)
    description = models.TextField(blank=True)
    price = models.IntegerField()
    bedrooms = models.IntegerField()
    bathrooms = models.DecimalField(max_digits=2, decimal_places=1)
    garage = models.IntegerField(default=0)
    sqft = models.IntegerField()
    lot_size = models.DecimalField(max_digits=5, decimal_places=1)
    photo_main = models.ImageField(upload_to="photos/%Y/%m/%d/")
    photo_1 = models.ImageField(upload_to="photos/%Y/%m/%d/", blank=True)
    photo_2 = models.ImageField(upload_to="photos/%Y/%m/%d/", blank=True)
    photo_3 = models.ImageField(upload_to="photos/%Y/%m/%d/", blank=True)
    photo_4 = models.ImageField(upload_to="photos/%Y/%m/%d/", blank=True)
    photo_5 = models.ImageField(upload_to="photos/%Y/%m/%d/", blank=True)
    photo_6 = models.ImageField(upload_to="photos/%Y/%m/%d/", blank=True)
    is_published = models.BooleanField(default=True)
    list_date = models.DateTimeField(default=datetime.now, blank=True)

    def __str__(self):
        return self.title
```

To add to the database, do then following:
1. run `python manage.py makemigrations <model_name>` (model name is optional)
2. run `python manage.py migrate`

### Create a SuperUser and Register models with Admin

#### Create a super user
* run `python manage.py createsuperuser` and follow the prompts to create an initial admin user

#### Register Models with Admin Backend
* Open the admin.py  for the app you want to register
* import the model `from .models import <model_name>`
* register the model `admin.site.register(<model_name>)`

#### Admin Customization
* Modify the admin template -- Create `templates/admin/base_site.html` with the following code as a guide.
```jinja
{% extends 'admin/base.html' %}

{% load static %}
{% block branding %}
  <h1 id='head'>
    <img src="{% static 'img/logo.png' %}" alt="BT Logo" class="brand_img" height="50" width="80">Admin Area
  </h1>
{% endblock branding %}
{% block extrastyle %}
<link rel='stylesheet' href={% static 'css/admin.css'%}>
{% endblock extrastyle %}
```
* Modify the the display of Models in the Admin area by creating a class inheirited from ModelAdmin
```python
class RealtorAdmin(admin.ModelAdmin):
    list_display = ('id', 'name', 'email', 'hire_date')
    list_display_links = ('id', 'name')
    search_fields = ('name', )
    list_per_page = 25
```

## Template Access to Model Data
* Import the model into the view that will display the template
* In the view query the model and save to a dictionary
* Pass the dictionary to the render function in the view
* format and display the data in the templat{{listing.bedrooms,-linklistingmvp{{}}
