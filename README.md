# Application Development Reviewer

## 1. Git Commands

**Initialize Repo**:  Create a local (computer-based) repository
>  git init

**Clone Repo**: Copy a remote (GitHub-based) repository into your local device
> git clone [GitHub URL]

**Check file status**: Check what files are ready to be added or committed
> git status

**Stage File**: Stage a file recently created, modified or deleted, and set it as ready to be committed
> git add .

**Commit Changes**: Save all changes made
> git commit -m "Commit Description

**Check Logs**: View commit history; '--oneline' makes it compact
> git log --oneline

**Create a branch**: Create a separate branch in local repo to host and test feature changes
> git branch [branch name]

**Checkout branch**: Switch to specified branch; -b creates a branch then switches to it
> git checkout -b [branch name]

**Merge branch**: Merge changes from one branch to another
> git merge [branch name]

**Delete local branch**: Delete a local branch
> git branch -d [branch name]

**Delete remote branch**: Delete a remote branch
>git push origin --delete [branch name]

**Push to remote**: Upload to GitHub
> git push origin [branch name]

**Pull to local**: Download changes made in remote repository
> git pull origin [branch name]

## 2. Python commands

**Install Packages**: Install existing packages like Django, Faker etc.
> pip install [package]

**Save installed packages**: Save package name and version in a text file
> pip freeze > filename.txt

**Install packages from a file**: Install multiple packages at once
> pip install -r filename.txt

**Create virtual environment**: Create virtual env that stores and handles dependencies
> python -m venv [virtual env name]

**Activate the virtual env**: Activate virtual env such that packages installed shall be located here. (Inside virtual env directory)
> Scripts\activate

## 3. Django commands

**Create new project**: Create the main folder for the django project
> django-admin startproject [project name]

**Create a new app**: Inside folder where 'manage.py' is, create a new app
> python manage.py startapp [app name]

**Run server**: Run and test a server to host application
> python manage.py runserver [IP]:[Port]

**Make migrations**: Checks all modifications made to database and models
> python manage.py makemigrations

**Migrate**: Migrate or apply changes made to database and models
> python manage.py migrate

**Create superuser**: Create admin user account on local project
> python manage.py createsuperuser

## 4. Markdown

**Heading**: `#Heading 1 to ######Heading 6`  
**Paragraph**: `P1 [space][enter][enter] P2`  
**Line break**: `L1 [space][space][enter] L2`  
**Emphasis**: `*Italic*, **Bold**, ***Combined***`  
**Links**: `(text)[link URI]`  
**Image**: `!(alt name)[img URI]`  
**Unordered list**: `+, -, or -`  
**Ordered list**: `Numbers`  
**Blockquote**: `>text`  
**Horizontal line**: `---, ***, or ___`  
**Single-line code**: `[backtick(x1)]code snippet[backtick(x1)]`  
**Multi-line code**: `[backtick(x3)]code snippet[backtick(x3)]`


## 5. Creating project (SetUp)
5.1 **Create environment**: 
> python -m venv [virtual env name] 

5.2 **Create remote repo then clone it inside environment**:
> cd [virtual env name]  
git clone [GitHub URL]

5.3 **Install Django**:
> Scripts\activate  
pip install Django  

5.4 **Create project**:
> cd [local repo name]  
django-admin startproject [project name] 

5.5 **Create application**:
> cd [project folder]  
python manage.py startapp [app name] 

5.6 **Register app in settings.py**:
> INSTALLED_APPS = ["django.cont..., "App name",] 

5.7 **Setup database**:
> python manage.py makemigrations  
python manage.py migrate 

5.8 **Test server**:
> python manage.py runserver  
*CTRL + C* 

## 6. Create models and Admin  
6.1 **Create models**:  
```
class BaseModel(models.Model):
    field = models.Datatype(params) 
    
    class Meta:
        abstract = True

class ModelName(BaseModel):
    field = models.Datatype(params)

    def __str__(self):
        return self.field
```  
6.2 **Migrate database changes**:
> python manage.py makemigrations  
python manage.py migrate 

6.3 **Register models in admin.py**:  
```
from .models import ModelName

admin.site.register(ModelName)
``` 

6.4 **Create superuser**:
> python manage.py createsuperuser 

6.5 **Refactor admin.py**:  
```
#Remove: admin.site.register(ModelName)

@admin.register(ModelName)
class ModelNameAdmin(admin.ModelAdmin):
    list_display = ("field1", "field2") #Visible columns
    search_fields = ("field1, "field2") #Search value in specified fields
    list_filter = ("field1", "field2") #Filter by specified fields
``` 

6.6 **Miscellaneous**:
> (1) pip freeze > requirements.txt  
(2) *Create README.md*  
(3) *Add and commit in between tasks*

## 7. Frontend  
7.1 **Static Files**:  
> (1) Create folder 'static' inside project folder  
(2) Store css, js, and img assets here  
(3) Link css using: `{% static '/css/stylesheet.css' %}`  

7.2 **Templates**:  
> (1) Create templates folder inside project folder  
(2) Setup includes folder inside templates  

7.3 **Forms**:  
> (1) Install widget tweaks: pip install django-widget-tweaks  
(2) Register widget tweaks in settings.py: `INSTALLED_APPS = ["django.cont..., "App name", "widget_tweaks",]`  
(3) Create form.html inside /includes folder  

(4) Edit form.html with your own html design and render forms using this django tags:  
```
{% load widget_tweaks %}

{% for field in form %}
<div>
    <label>{{ field.label_tag }}</label>
    <div>
        {% render_field field class="form-control" %}
    </div>

    {% for error in field.errors %}
    <div>
        {{ error }}
    </div>
</div>
{% endfor %}
```

> `{% load widget_tweaks %}` : Imports widget tweaks functionalities  
`{% for field in form %}...{% endfor %}`: Loops through all fields specified in forms.py  
`{{ field.label_tag }}`: Calls and loads the current field/variable name  
`{% render_field field class="form-control" %}`: Loads an input tag with the appropriate type. (Ex: type='text' for models.Charfield)  
`{% for error in field.errors %}...{% endfor %}`: Loops through all errors during input  
`{{ error }}`: Loads the error  

7.4 **Pagination**:  
> (1) Create pagination.html inside /includes folder  

(2) Edit pagination.html using these tags:  
```
{% if is_paginated %}
<ul>
    {% if page_obj > 1 %}
    <li>
        <a href="?page=1">First</a>
    </li>

    {% else %}
    <li class="disabled">
        <span>First</span>
    </li>
    {% endif %}

    {% if page_obj.has_previous %}
    <li>
        <a href="?page={{ page_obj.previous_page_number }}">Prev</a>
    </li>   

    {% else %}
    <li class="disabled">
        <span>Prev</span>
    </li>
    {% endif %}  

    {% for page_num in paginator.page_range %}
        {% if page_obj.number == page_num %} 
        <li>
            <span>{{ page_num }}</span>
        </li>

        {% elif page_num > page_obj.number|add:'-3' and page_num < page_obj.number|add:'3' %}
        <li>
            <a href="?page={{ page_num }}">{{ page_num }}</a>
        </li>
        {% endif %}
    {% endfor %}

    {% if page_obj.has_next %}
    <li>
        <a href="?page={{ page_obj.next_page_number }}">Next</a>
    </li>   

    {% else %}
    <li class="disabled">
        <span>Next</span>
    </li>
    {% endif %}  

    {% if page_obj.number != paginator.num_pages %}
    <li>
        <a href="?page={{ paginator.num_pages }}">Last</a>
    </li>  

    {% else %}
    <li class="disabled">
        <span>Last</span>
    </li>
    {% endif %}
</ul>
<p>{{ object_list.count }} out of {{ paginator.count }}</p>
{% endif %}
``` 

> `{% if is_paginated %}`: Checks views.py if 'paginate_by' is set for a model  
`{% if page_obj > 1 %}...{% endif %}`: Checks if the current page is not the first page  
`{% if page_obj.has_previous %}...{% endif %}`: Checks if the current page has a previous page  
`{{ page_obj.previous_page_number }}`: Call and set the previous page number value as the link href.  
`{% for page_num in paginator.page_range %}...{% endfor %}`: Loops throug all page numbers  
`{% if page_obj.number == page_num %}...{% endif %}`: Check if the looped number is the current page number selected; if true, disabling this tag is suggested  
`{% elif page_num > page_obj.number|add:'-3' and page_num < page_obj.number|add:'3' %}`: Checks if the current page number has at least two pages behind and in front of it; if true, load a page button for them  
`{{ page_num }}`: Call the current value of page_num in the loop  
`{% if page_obj.has_next %}...{% endif %}`: Checks if current page has a next page number  
`{{ page_obj.next_page_number }}`: Call and set the next page number value as the link href  
`{% if page_obj.number != paginator.num_pages %}`: Check if current page is not the maximum (last) page  
`{{ paginator.num_pages }}`: Count of all page numbers  
`{{ object_list.count }}`: Count of rows presented in the current page  
`{{ paginator.count }}`: Count of all records

7.5 **Template Tags**:  
`{{ variable }}`: Calling a variable using django tags.  
`{% load static %}`: Loads static files: img, css, js.  
`{% block [block name] %}(empty){% endblock %}`: Allocates an empty space (placeholder) to insert contents of other html files; usually written in base.html (parent html of other html).    
`{% extends 'base.html' %}{% block [block name] %}...{% endblock%}`: Fills in the {% block [block name] %}...{% endblock %} by matching the child block name to the parent block name.  

7.6 **Mapping template and static folders**:  
(1) Modify settings.py:  
```
import os

TEMPLATES = [
    {
        "BACKEND": "djan...
        "DIRS": [os.path.join(BASE_DIR, 'templates')],
        "APP_D...
    }
]

STATIC_URL = 'static/'
STATIC_ROOT = BASE_DIR / 'staticfiles'
STATICFILES_DIRS = (BASE_DIR / 'static',)

#This code snippet tells the system where the templates and static folders are located such that tags ({}) can be used.
```


## 8.Views
8.1 **ListView**

> (1) Views.py  
```
from django.views.generic.list import ListView
from appName.models import ModelName

class ModelNameListView(ListView):
    model = ModelName  
    context_object_name = 'chosenViewName'  
    template_name = 'Modellist.html'
    paginate_by = number
```

> (2) URLS.py  
```
from appName.views import ModelNameListView

urlpatterns = [
    path('endpoint_name', ModelNameListView.as_view(), name='chosenURLName',)
]
```

> (3) Home.html
```
<a href="{% url 'chosenURLName' %}">
```

> (4) Design Modellist.html

8.2 **CreateView**

> (1) Views.py  
```
from django.views.generic.edit import CreateView
from appName.forms import ModelForm
from django.urls import reverse_lazy

class ModelNameCreateView(CreateView):
    model = ModelName  
    form_class =  ModelForm
    template_name = 'modelForm.html'
    success_url = reverse_lazy('chosenURLName')
```

>(2) Forms.py
```
from django.forms import ModelForm
from django import forms
from .models import ModelName

class ModelNameForm(ModelForm):
    class Meta:
        model = ModelName
        fields = "__all__"
```

> (3) URLS.py  
```
from appName.views import ModelNameListView, ModelNameCreateVIew

urlpatterns = [
    path('endpoint_name/add', ModelNameCreateView.as_view(), name='chosenURLName-add',)
]
```

> (4) Modellist.html
```
<a href="{% url 'chosenURLName-add' %}">Add</a>
```

> (5) Design modelForm.html and inside the form tag, write this: 
```
{% csrf_token %}{% include 'includes/form.html' %}
```


8.3 **UpdateView**
> (1) Views.py  
```
from django.views.generic.edit import CreateView, UpdateView

class ModelNameUpdateView(UpdateView):
    model = ModelName  
    form_class =  ModelForm
    template_name = 'modelForm.html'
    success_url = reverse_lazy('chosenURLName')
```

> (2) URLS.py    
```
from appName.views import ModelNameListView, ModelNameCreateVIew, ModelUpdateView

urlpatterns = [
    path('endpoint_name/<pk>', ModelNameUpdateView.as_view(), name='chosenURLName-edit',)
]
```

> (3) Modellist.html
```
<a href="endpoint_name/{{ object.id }}">Add</a>
```  

8.4 **DeleteView**  
> (1) Views.py  
```
from django.views.generic.edit import CreateView, UpdateView, DeleteView

class ModelDeleteView(DeleteView):
    model = ModelName  
    template_name = 'modelDel.html'
    success_url = reverse_lazy('chosenURLName')
```

> (2) URLS.py
```
from appName.views import ModelNameListView, ModelNameCreateVIew, ModelUpdateView, ModelDeleteView

urlpatterns = [
    path('endpoint_name/<pk>/delete', ModelDeleteView.as_view(), name='chosenURLName-delete',)
]
```

> (3) Modellist.html
```
<a href="endpoint_name/{{ object.id }}/delete">Add</a>
```  

> (4) Design modelDel.html then inside the form tag, add this:  
```
{% csrf_token %}{% include 'includes/form.html' %}
```

## 9. Search, Context data and Sort
9.1 **Search/Filter** 
> (1) modellist.html  
```
<form action="{% url 'chosenURLName' %}">
    <input type='text' name='q'>
</form>
```

> (2) **Views.py**  
```
from django.db.models import Q

class ModelNameListView(ListView):

    def get_queryset(self):
        qs = super().get_queryset()
        query = self.request.GET.get('q')

        if query:
            qs = qs.filter(
                Q(field__icontains=query)
            )
```

9.2 **Context data**
> (1) Views.py  
```
from django.utils import timezone

class ModelNameListView(ListView):

    def get_context_data(self, **kwargs):

        context = super().get.context_data(**kwargs)
        context["key"] = ModelName.objects.count()
        
        return context
```

> (2) Home.html or any html  
```
{{ key }}
```

9.3 **Sorting**
> (1) Static (fixed)  
```
class ModelNameListView(ListView):
    ordering = ["field1", "field2"]
```

> (2) Dynamic  
```
class ModelNameListView(ListView):

    def get_ordering(self):
        allowed = ["field1", "field2"]
        sort_by = self.request.GET.get("sort_by")

        if sort_by in allowed:
            return sort_by

        return "field1"
```

## 10. Login Auth and Socials
> (1) Install dependencies:  
pip install django-allauth
pip install requests
pip install PyJWT
pip install cryptography

> (2) Settings.py
```
INSTALLED_APPS = [
    ...,
    'django.contrib.sites',
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'allauth.socialaccount.providers.google',
    'allauth.socialaccount.providers.github',
]

SITE_ID = 2
AUTHENTICATION_BACKENDS = [
'django.contrib.auth.backends.ModelBackend',
'allauth.account.auth_backends.AuthenticationBackend',
]

MIDDLEWARE = [
    ...,
    'allauth.account.middleware.AccountMiddleware',
    ...
]

LOGIN_URL = '/accounts/login/'
LOGIN_REDIRECT_URL = '/' 
LOGOUT_REDIRECT_URL = '/accounts/login/' 
ACCOUNT_LOGOUT_REDIRECT_URL = '/' 
ACCOUNT_LOGOUT_ON_GET = True
ACCOUNT_LOGIN_METHODS = {"username", "email"}
ACCOUNT_SIGNUP_FIELDS = [
    "username*",
    "email*",
    "password1*",
    "password2*",
]
```

> (3) URLS.py
```
from django.urls import path, include

urlpatterns = [
    path("accounts/", include("allauth.urls")),
]
```

> (4) Go to https://console.cloud.google.com/ -> APIs & Services -> Credentials  
(5) Create credentials -> OAuth 2.0 Client ID  
(6) Select 'Web Application' for Application type  
(7) Set the Client Name  
(8) Set the Authorized redirect URIs to: http://127.0.0.1:8000/accounts/google/login/callback/  
(9) Confirm all then save Client ID and Client Secret  
(10) Run server then go /admin  
(11) Add Social Applications with the following inputs:  
Provider: Google  
Name: Google Login  
Client ID: paste  
Secret: paste  
Sites: 127.0.0.1:8000  
(12) Run migrations; makemigrations and migrate  
(13) Create and design templates/account/login.html  
(14) Create and design templates/socialaccount/login.html
