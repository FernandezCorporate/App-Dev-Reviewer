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



