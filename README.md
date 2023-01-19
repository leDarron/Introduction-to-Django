# Workshop - Introduction to Django

- Learn the basics of Django (https://www.djangoproject.com/)
- Create your first Website with this programming language !

# Step 0: Initialization of the project

After this tutorial, you will have a basic poll application in two part :

- A public site that lets people view polls and vote in them.

- An admin site that lets you add, change, and delete polls.

to be sure that you have django Installed, write :

`python -m django --version`
, if not : go to [SETUP.md](./SETUP.md)

Now that you have Django installed, create your first project :

`django-admin startproject mysite`
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

- **mysite/**init**.py:** An empty file that tells Python that this directory should be considered a Python package.

- **mysite/settings.py:** Settings/configuration for this Django project.

- **mysite/urls.py: ** he URL declarations for this Django project; a “table of contents” of your Django-powered site.

- **mysite/asgi.py:** An entry-point for ASGI-compatible web servers to serve your project.

- **mysite/wsgi.py:** An entry-point for WSGI-compatible web servers to serve your project.

# Step 1: The server

You can now launch your server with the command :

`python manage.py runserver`

If it's all working, you should have "Congratulations!" at http://127.0.0.1:8000/

Now, you can create your app with the command :

`python manage.py startapp polls`

that will create a directory polls.

# Step 2: Your first view

Create your first view in the directory polls, and write : "you are at the polls index.". If everything works, you should have this sentence at `http://localhost:8000/polls/`

Result preview :

![image](https://user-images.githubusercontent.com/72023512/213476136-1a5cf85d-3d5a-435a-b147-75cf50a35b32.png)

# Step 3: Creating models

In our poll app, we’ll create two models: Question and Choice. A Question has a question and a publication date. A Choice has two fields: the text of the choice and a vote tally. Each Choice is associated with a Question.

These concepts are represented by Python classes. Edit the polls/models.py to do it !

After that, edit the file mysite/settings.py, so it looks like that :

```
INSTALLED_APPS = [
    'polls.apps.PollsConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

execute the function :
`python manage.py makemigrations polls` and `python manage.py migrate` , You should see something similar to the following:

```Migrations for 'polls':
  polls/migrations/0001_initial.py
    - Create model Question
    - Create model Choice
```
