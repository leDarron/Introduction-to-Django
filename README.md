# Workshop - Introduction to Django
- Learn the basics of Django (https://www.djangoproject.com/)
- Create your first Website with this programming language !

# Step 0: Initialization of the project 
After this tutorial, you will have a basic poll application in two part : 
- A public site that lets people view polls and vote in them.

- An admin site that lets you add, change, and delete polls.

to be sure that you have django Installed, write :

``` python -m django --version ``` 
, if not : go to [SETUP.md](./SETUP.md)


Now that you have Django installed, create your first project :

``` django-admin startproject mysite ``` 
, where "mysite" is the name of your site.

You should have : 
```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
        
```
These files are:

- **The outer mysite/** root directory is a container for your project. Its name doesn’t matter to Django; you can rename it to anything you like.

- **manage.py:** A command-line utility that lets you interact with this Django project in various ways.

- **The inner mysite/** directory is the actual Python package for your project. Its name is the Python package name you’ll need to use to import anything inside it (e.g. mysite.urls).

- **mysite/__init__.py:** An empty file that tells Python that this directory should be considered a Python package.

- **mysite/settings.py:** Settings/configuration for this Django project.


- **mysite/urls.py: ** he URL declarations for this Django project; a “table of contents” of your Django-powered site. 


- **mysite/asgi.py:** An entry-point for ASGI-compatible web servers to serve your project.


- **mysite/wsgi.py:** An entry-point for WSGI-compatible web servers to serve your project.


# Step 1: The server

You can now launch your server with the command : 

``` python manage.py runserver ```

If it's all working, you should have "Congratulations!" at http://127.0.0.1:8000/
