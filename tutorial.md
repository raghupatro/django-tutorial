# basic Django tutorial

## to create basic folder structure

1. `git init`
2. create .gitignore, README.md
3. create venv `python -m venv venv`
4. add venv/ to .gitignore
5. install required dependencies `pip install Django`
6. save dependencies list in a file `python -m pip freeze > requirements.txt`
7. add and commit changes

## part 1: to create a basic Django project (as per docs)

1. `django-admin startproject mysite` creates a base project
2. `python manage.py runserver` to run the website
3. `python manage.py startapp polls` to create a new polls app
4. create a view in the _polls/views.py_ file

```
    from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```

5. create a _polls/urls.py_ file, to add url of the app

```
from . import views

urlpatterns = [
    path("", views.index, name="index"),
]
```

6. add the `import()` statement in the _mysite/urls.py_ file

```
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path("polls/", include("polls.urls")),
    path('admin/', admin.site.urls),
]
```

7. runserver

## part 2: database setup and django admin

1. _mysite\settings.py_ has all settings, change database settings according to requirements
2. `python manage.py migrate` to create the tables(req for any of the Django applications) in the database
3. create your Question and Answer data models in _polls/models.py_

```
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField("date published")


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

4. tell our project that the polls app is installed, add 'polls.apps.PollsConfig' to _mysite/settings.py_
5. tell django that changes are made to the models, make migration for the polls app `python manage.py makemigrations polls`
6. run `python manage.py sqlmigrate polls 001` to check the sql code Django will run on migrating
7. run migration `python manage.py migrate`
8. `python manage.py shell` opens the interactive python shell
9. make changes in the model as required, after interacting with the model in the shell

### Admin

1. create an admin `python manage.py createsuperuser`
   admin
   admin@example.com
   12345
2. edit _polls/admin.py_ to tell django that Questions have an admin interface

```
from django.contrib import admin

from .models import Question

admin.site.register(Question)
```

## part 3: writing your first Django app

1.
