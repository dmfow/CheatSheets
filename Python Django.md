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
python manage.py runserver 0.0.0.0:8000
# Surf to http://127.0.0.1:8000 or http://YOURIP:8000
# Read more here: https://docs.djangoproject.com/en/5.1/intro/tutorial01/

```

## User handling
#### ... 
```
# https://learndjango.com/tutorials/django-login-and-logout-tutorial

# A. django_project/urls.py
from django.contrib import admin
from django.urls import path, include  # new

urlpatterns = [
    path("admin/", admin.site.urls),
    path("accounts/", include("django.contrib.auth.urls")),  # new
]

# B. at the linux promt $ (in the projects root directory - same as where manage.py reside)
mkdir templates
mkdir templates/registration

# C. edit/create: templates/registration/login.html
<!-- templates/registration/login.html -->
<h2>Log In</h2>
<form method="post">
  {% csrf_token %}
  {{ form }}
  <button type="submit">Log In</button>
</form>

# D. edit: django_project/settings.py
TEMPLATES = [
    {
        ...
        "DIRS": [BASE_DIR / "templates"],  # new
        ...
    },
]


# E. Edit: django_project/settings.py (add to bottom of the file)
LOGIN_REDIRECT_URL = "/"  # new




```


