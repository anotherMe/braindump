# Django installation and simple app creation

Target system: Debian Jessie stable

Reference: [[https://docs.djangoproject.com/en/1.10/intro/tutorial01/|Writing your first Django app, part 1]]

## System setup

  # apt install virtualenv
  # apt install python-pip


## Setup virtualenv (Python3)

  # mkdir /opt/virtualenv
  # chown -R <MYUSER>:users /opt/virtualenv
  $ virtualenv /opt/virtualenv/<MYVENV> -p /usr/bin/python3
  $ source /opt/virtualenv/<MYVENV>/bin/activate


## Install Django

  (<MYVENV>)$ pip install django


## Create the project

  (<MYVENV>)$ django-admin startproject <MYPROJECT>

## Create the app

  (<MYVENV>)$ python manage.py startapp <MYAPP>


## Setup database

Create and apply migrations for the *INSTALLED_APPS* (not many at the moment):

  (<MYVENV>)$ python manage.py makemigrations
  (<MYVENV>)$ python manage.py migrate

Possibly, create superuser to access the //admin// section of the site:

  (<MYVENV>)$ python manage.py createsuperuser


## Test project
  
  (<MYVENV>)$ cd <MYPROJECT>
  (<MYVENV>)$ python manage.py runserver

Or, if you want to listen on external addresses and/or change port:

  (<MYVENV>)$ python manage.py runserver 0.0.0.0:8000
