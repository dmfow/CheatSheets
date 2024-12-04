#### Install
```
# On Linux prompt $
# 1. Install Django
pip install Django
## 2. Add django-admin to PATH (see instrucions under Alpine or Ubuntu)
# 3. Test
mkdir djangotutorial
cd djangotutorial
django-admin startproject mytestsite djangotutorial
# mytestsite = [projectname]
python manage.py runserver 0.0.0.0:8000
# Surf to http://127.0.0.1:8000 or http://YOURIP:8000
# Read more here: https://docs.djangoproject.com/en/5.1/intro/tutorial01/

# also install python package: tzdata
pip install tzdata
```

#### Configure a website with user login, logout
```
# https://learndjango.com/tutorials/django-login-and-logout-tutorial

# A. [projectname]/urls.py
from django.contrib import admin
from django.urls import path, include  # new

urlpatterns = [
    path("admin/", admin.site.urls),
    path("accounts/", include("django.contrib.auth.urls")),  # new
]

# B. If needed (depending on the setup). Add to settings.py. Change localhost you your hostname or IP address if needed
ALLOWED_HOSTS = ['localhost']

# C. at the linux promt $ (in the projects root directory - same as where manage.py reside)
mkdir templates
mkdir templates/registration

# D. edit/create: templates/registration/login.html
<!-- templates/registration/login.html -->
<h2>Log In</h2>
<form method="post">
  {% csrf_token %}
  {{ form }}
  <button type="submit">Log In</button>
</form>

# E. edit: [projectname]/settings.py
TEMPLATES = [
    {
        ...
        "DIRS": [BASE_DIR / "templates"],  # new
        ...
    },
]


# F. Edit: [projectname]/settings.py (add to bottom of the file)
LOGIN_REDIRECT_URL = "/"  # new

# G. Create a superuser account. At prompt $
python manage.py migrate
python manage.py createsuperuser
# H. If needed (depending on the setup). Add to settings.py
CSRF_TRUSTED_ORIGINS = ['http://localhost:8000'],
CORS_ORIGIN_WHITELIST = ['http://localhost:8000']
ALLOWED_HOSTS = ['localhost']

# I. Restart the django server
# J. Surf to: http://127.0.0.1:8000/accounts/login/ and login
# K. Create a "homepage" with some templates
<!-- templates/base.html -->
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>{% block title %}Django Auth Tutorial{% endblock %}</title>
</head>

<body>
  <main>
    {% block content %}
    {% endblock %}
  </main>
</body>

</html>

<!-- templates/home.html -->
{% extends "base.html" %}

{% block title %}Home{% endblock %}

{% block content %}
{% if user.is_authenticated %}
Hi {{ user.username }}!
{% else %}
<p>You are not logged in</p>
<a href="{% url 'login' %}">Log In</a>
{% endif %}
{% endblock %}


<!-- templates/registration/login.html -->
{% extends "base.html" %}

{% block title %}Login{% endblock %}

{% block content %}
<h2>Log In</h2>
<form method="post">
  {% csrf_token %}
  {{ form }}
  <button type="submit">Log In</button>
</form>
{% endblock %}


# L. Update: django_project/urls.py
from django.contrib import admin
from django.urls import path, include
from django.views.generic.base import TemplateView  # new

urlpatterns = [
    path("admin/", admin.site.urls),
    path("accounts/", include("django.contrib.auth.urls")),
    path("", TemplateView.as_view(template_name="home.html"), name="home"),  # new
]

# M. Test login, then go to: http://127.0.0.1:8000/admin/ and logout

# N. Add logout button (edit templates/home.html and [projectname]/settings.py)

<!-- templates/home.html-->
{% extends "base.html" %}

{% block title %}Home{% endblock %}

{% block content %}
{% if user.is_authenticated %}
Hi {{ user.username }}!
<form action="{% url 'logout' %}" method="post">
  {% csrf_token %}
  <button type="submit">Log Out</button>
</form>
{% else %}
<p>You are not logged in</p>
<a href="{% url 'login' %}">Log In</a>
{% endif %}
{% endblock %}

# django_project/settings.py
LOGIN_REDIRECT_URL = "home"
LOGOUT_REDIRECT_URL = "home"



```


