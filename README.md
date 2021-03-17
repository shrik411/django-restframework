# django-restframework
Step by step guide from docker to serialization and views

## docker file

```
FROM python:3

ENV PYTHONUNBUFFERED=1

WORKDIR /app

COPY . /app

RUN pip install -r requirements.txt
```

## docker compose

```
version: "3.9"

services: 
    db:
      image: postgres
      environment:
        - POSTGRES_DB=postgres
        - POSTGRES_USER=postgres
        - POSTGRES_PASSWORD=postgres
      volumes:
        - ./postgres-data:/var/lib/postgresql/data

    web:
      build: ./api/
      command: python manage.py runserver 0.0.0.0:8000
      volumes:
        - ./api:/app
      ports:
        - "8000:8000"
      depends_on:
        - db

```

## Create a Django project

```
docker-compose run web django-admin startproject newproject .
```

### Make sure to change DATABSE -> default entry in settings if we not using sqlite
```
   
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'PASSWORD': 'postgres',
        'HOST': 'db',
        'PORT': 5432,
    }
}
```

## requirements.txt

```
asgiref==3.2.7
certifi==2020.6.20
cffi==1.14.0
chardet==3.0.4
cryptography==2.9.2
defusedxml==0.7.0rc1
discord-webhook==0.9.0
Django==3.0.7
django-braces==1.14.0
django-cors-headers==3.4.0
django-debug-toolbar==2.2
django-oauth-toolkit==1.3.2
django-rest-framework-social-oauth2==1.1.0
djangorestframework==3.11.0
drf-nested-routers==0.91
flake8==3.8.3
idna==2.10
importlib-metadata==1.6.1
mccabe==0.6.1
oauthlib==3.1.0
Pillow==7.1.2
psycopg2==2.8.5
pycodestyle==2.6.0
pycparser==2.20
pyflakes==2.2.0
PyJWT==1.7.1
python3-openid==3.2.0
pytz==2020.1
requests==2.24.0
requests-oauthlib==1.3.0
six==1.15.0
social-auth-app-django==4.0.0
social-auth-core==3.3.3
sqlparse==0.3.1
urllib3==1.25.9
zipp==3.1.0
```

## Create new app

```
django-admin startapp quickstart
```
