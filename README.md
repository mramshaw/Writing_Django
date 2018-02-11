# Writing Django

Having only used the `flask` framework, I thought it might be fun to check out Python's Django framework.

As far as I can tell, it is a heavy-weight framework very much like PHP's Laravel.

## Pre-requisites

Python is required, also a package manager (either `pip` or `pip3`) appropriate to the Python version.

Verify the installed version of Python as follows:

    $ python --version

[Python 2.7.12 in my case.]

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

## Credits

Part 1:

    https://docs.djangoproject.com/en/1.11/intro/tutorial01/

Part 2:

    https://docs.djangoproject.com/en/1.11/intro/tutorial02/
