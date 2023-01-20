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

# Step 4: create the polls and the choices with the python shell

first step : write `python manage.py shell`

after that, with the shell, find a way to create the polls and the choices. You can do the number of polls that you want and at least 2 choices per polls. At the end, it's should look like that :

```
>>> Question.objects.all()
<QuerySet [<Question: Question object (1)>]>

>>> q.choice_set.count()
3 (if you have 3 choices)
```

# Step 5: Creating an admin user

```
python manage.py createsuperuser

Username: admin
Email address: admin@example.com
Password: **********
Password (again): *********
Superuser created successfully.
```

Now, start your server and go to "/admin". you should have that :

![image](https://user-images.githubusercontent.com/72023512/213755617-b1240fd2-6c70-4dd6-9bb0-ef7718f4b7c3.png)

to make the poll modifiable by the admin, add that to polls/admin.py :

```
from django.contrib import admin

from .models import Question

admin.site.register(Question)

```

Now you should have the "POLLS" option available :

![image](https://user-images.githubusercontent.com/72023512/213755869-ee1b9990-e949-48be-931a-1a5166b9ea5b.png)

# Step 6: write more views

write veiws for the detail, the results and the vote. You should uptdate the file polls/views.py and polls/urls.py

After that, you can add a simple front in a new directory **polls/templates/polls/index.html** that should look like that :

```
{% if latest_question_list %}
    <ul>
    {% for question in latest_question_list %}
        <li><a href="/polls/{{ question.id }}/">{{ question.question_text }}</a></li>
    {% endfor %}
    </ul>
{% else %}
    <p>No polls are available.</p>
{% endif %}
```

# Step 7: Write a 404 error

Raise a 404 error if the polls is not existing. It should be in your polls/views.py file.

# Step 8: write your front for the detail and result

In your polls/views.py : add a function to vote. It should look like that :

```

def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        return render(request, 'polls/detail.html', {
            'question': question,
            'error_message': "You didn't select a choice.",
        })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        return HttpResponseRedirect(reverse('polls:results', args=(question.id,)))

```

Now create a .html for the detail and result.

# Conclustion

If everything is working, you now can vote for everyting. If you want to continue, you can ameliorate the vote system or the front.
