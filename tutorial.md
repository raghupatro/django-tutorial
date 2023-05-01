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

4.
