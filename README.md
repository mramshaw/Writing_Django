# Writing Django

Having only used the `flask` framework, I thought it might be fun to check out Python's Django framework.

As far as I can tell, it is a heavy-weight framework very much like PHP's Laravel.

## Pre-requisites

Python is required, also a package manager (either `pip` or `pip3`) appropriate to the Python version.

Verify the installed version of Python as follows:

    $ python --version

[Python 2.7.12 in my case. Don't worry about version issues, Django will create needed `__future__` import statements auto-magically.]

Install the latest version of Django (plus dependencies) as follows:

    $ pip install --user django

[Replace `pip` with `pip3` as appropriate.]

[The dependency Python Time Zone module `pytz` will also be installed.]

Verify the installed version of Django as follows:

    $ python -m django --version

[Version 1.11.10 in my case.]

## Create a Project

Use the `django-admin` command to do this:

    $ django-admin startproject polls

Note that [django-admin](https://docs.djangoproject.com/en/1.11/ref/django-admin/)
 creates a folder plus infra-structure files, much like `maven` or `sbd`.

Lets check the development server works:

    $ cd polls
    $ python manage.py runserver

The results should be something like:

    Performing system checks...
    
    System check identified no issues (0 silenced).
    
    You have 13 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
    Run 'python manage.py migrate' to apply them.
    
    February 11, 2018 - 21:43:01
    Django version 1.11.10, using settings 'polls.settings'
    Starting development server at http://127.0.0.1:8000/
    Quit the server with CONTROL-C.
    ^Cpolls$

The development server at http://127.0.0.1:8000/ should look something like:

![Development_Server](images/Development_Server.png)

## Projects versus Apps

A project is mostly concerned with a website, whereas an app is mostly concerned with an application (or `microservice` if you will).

An app can live anywhere, but for the sake of convenience we will create this one in our current project.

## Create an App

This needs to be done in the folder where `manage.py` lives:

    $ python manage.py startapp polls-app

And if, like me, you are from a polyglot background, you will now get a reminder
that Python prefers underscores to hyphens:

    CommandError: 'polls-app' is not a valid app name. Please use only numbers, letters and underscores.
    $

So lets get with the program:

    $ python manage.py startapp polls_app

This will create a `polls_app` folder, plus files.

## Create a View

Open `polls_app\views.py` and change it as follows:

    $ diff -uw views.py.orig views.py
    --- views.py.orig	2018-02-11 14:18:23.894106000 -0800
    +++ views.py	2018-02-11 14:25:03.776911375 -0800
    @@ -3,4 +3,7 @@
     
     from django.shortcuts import render
     
    -# Create your views here.
    +from django.http import HttpResponse
    +
    +def index(request):
    +    return HttpResponse("Hello, world. You're at the polls index.")
    $

Create a `polls_app\urls.py` file and change it as follows:

    # -*- coding: utf-8 -*-
    from __future__ import unicode_literals
    
    from django.conf.urls import url
    
    from . import views
    
    urlpatterns = [
        url(r'^$', views.index, name='index'),
    ]

Next update the `polls\urls.py` file as follows:

    $ diff -uw urls.py.orig urls.py
    --- urls.py.orig	2018-02-11 14:37:19.727374508 -0800
    +++ urls.py	2018-02-11 14:45:15.909210776 -0800
    @@ -13,9 +13,11 @@
         1. Import the include() function: from django.conf.urls import url, include
         2. Add a URL to urlpatterns:  url(r'^blog/', include('blog.urls'))
     """
    +from django.conf.urls import include
     from django.conf.urls import url
     from django.contrib import admin
     
     urlpatterns = [
    +    url(r'^polls/', include('polls_app.urls')),
         url(r'^admin/', admin.site.urls),
     ]
    $

Again, lets check to see if everything works:

    $ python manage.py runserver

The polls app at http://127.0.0.1:8000/polls/ should look as follows:

![polls](images/polls.png)

The admin interface at http://127.0.0.1:8000/admin/ should look as follows:

![admin](images/admin.png)

And our development server at http://127.0.0.1:8000/ should now look like:

![404](images/404.png)

[END OF PART 1]

## Credits

Part 1:

    https://docs.djangoproject.com/en/1.11/intro/tutorial01/

Part 2:

    https://docs.djangoproject.com/en/1.11/intro/tutorial02/
