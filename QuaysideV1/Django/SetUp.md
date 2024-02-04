# Setting Up Django
**2/3/2024 • Mya Schroder**

## Setting up
First I made a venv and installed django. Then to set up django, I just followed the first couple steps of [this](https://docs.djangoproject.com/en/5.0/intro/tutorial01/) tutorial inside a venv. 
```bash
django-admin startproject quayside

cd quayside
python manage.py startapp app
python manage.py startapp api

```

As for why I chose the file structure...

First I looked up some good options:

* https://django-project-skeleton.readthedocs.io/en/latest/structure.html
* https://medium.com/django-unleashed/django-project-structure-a-comprehensive-guide-4b2ddbf2b6b8
* https://medium.com/@akshatgadodia/a-comprehensive-guide-to-structuring-django-projects-best-practices-and-example-afb77d8497d5  

For this project, we want to start off with a REST API that can be accessed both internally by our webapp as well as externally if needed. So then I asked ChatGPT, how to create a file structure for this, and it suggested:
```
quayside_project/
    ├── quayside_app/
    │   ├── migrations/
    │   ├── static/
    │   ├── templates/
    │   ├── admin.py
    │   ├── apps.py
    │   ├── models.py
    │   ├── tests.py
    │   ├── urls.py
    │   └── views.py
    ├── quayside_api/
    │   ├── migrations/
    │   ├── admin.py
    │   ├── apps.py
    │   ├── models.py
    │   ├── serializers.py
    │   ├── tests.py
    │   ├── urls.py
    │   └── views.py
    ├── quayside_project/
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    ├── manage.py
    └── requirements.txt
```

This higher level folders seemed like a good idea, so we went with it. 


## Tailwind
We chose to continue using Tailwind CSS so to add it to django, I used [this tutorial](https://flowbite.com/docs/getting-started/django/). This lets you only "download" the tailwind classes you use to output.css when you use them so you don't have to load the whole tailwind library when you usee quayside. Note: it needs npm.

However, I wanted most the tailwind static files just in the app folder, so I made these adjustments to the steps:

STEP 2:
    Added this instead: `"DIRS": [BASE_DIR / 'app' / 'templates'],`

STEP 5:
    Added this instead: 

    ```bash
    COMPRESS_ROOT = BASE_DIR / 'app' / 'static'
    COMPRESS_ENABLED = True
    STATICFILES_FINDERS = ('compressor.finders.CompressorFinder',)
    ```

STEP 6: 
    Did this in the app/static/src folder.

STEP 9-10:
    Did this in the app/templates folder.

Install Tailwind STEP 4:
    Ran the following command instead `npx tailwindcss -i ./app/static/app/src/input.css -o ./app/static/app/src/output.css --watch`


I attempted to put tailwind.config.js in the app/ directory as well, but found out after way to much fighting with the content file path, that it only likes being at the project root file directory. If it's not in the project root, it won't detect the tailwind classes in your html files (even if added relatively or absolutely to the content array) and will therefore not add the class references to output.css. 

For tailwind, you have to run `npx tailwindcss -i ./app/static/app/src/input.css -o ./app/static/app/src/output.css --watch` every time along with `python manage.py runserver` when want to start the server and edit Tailwind CSS (the first command looks for new Tailwind CSS class and adds them to `output.css`).
I was lazy and did not want to run both commands every time so I added a new django command to use to run both. I used chatGPT and [this tutorial](https://simpleisbetterthancomplex.com/tutorial/2018/08/27/how-to-create-custom-django-management-commands.html) so that when you run `python manage.py rundev`, it runs both.


For automatic CSS reload without refreshing the browser, I installed django-browser-reload and followed the last 4 commands of [this article](https://blog.devgenius.io/django-tailwind-setup-made-easy-36043adda97c). 


## Static Files
In my adventure with tailwind, I learned way more than I wanted about static files. Static folders are where you can put images, css, html, or any other static content.For static folders within apps [this](https://docs.djangoproject.com/en/5.0/howto/static-files/) is a good reference. A weird find I came across is that when you put static/ folder within an app (not just a project), you'll put a folder within the app with the apps name (ex/ `quayside/app/static/app/<staticFiles>`). This is because in production, all the static files from different apps are combined into 1 static folder, and django does not want to confuse the files.

 **Note for Future Self**: when serving django in production, you have to run `django-admin collectstatic` to combine static files into one big folder.


## requirements.txt
Finally, to save installed libraries, I ran `pip freeze > requirements.txt`