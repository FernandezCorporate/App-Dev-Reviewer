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
`{{ page_obj.previous_page_number }}`: Call and set the next page number value as the link href  
`{% if page_obj.number != paginator.num_pages %}`: Check if current page is not the maximum (last) page  
`{{ paginator.num_pages }}`: Count of all page numbers  
`{{ object_list.count }}`: Count of rows presented in the current page  
`{{ paginator.count }}`: Count of all records

