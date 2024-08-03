
# Connecting Django with Postgresql

Hi guys , I'm Ali seyfi Python Backend Developer and in this repository we are going to connect the django application to
the postgresql database .
I hope it will be usefull for you !

## 1- Download and install the postgresql database server

At first you should have the PostgreSQL database server on your operating system
Download and install the PostgreSQL from it's official website from link below:

[Download](https://www.postgresql.org/download/)

### if you are on Linux - Ubuntu distribution here is the command that you can run to download and  install the postgresql

~~~bash
sudo apt install postgresql
~~~

&nbsp;

## 2- Creating a new user and a new Database

At the second step you have to create a new user and a database for your django project. these are the tasks we are going to do with each other:

+ creating new user
+ creating new database
+ changing the owner of that database
+ give the all permissions to that user and owner

### so let's start and connect to postgresql in your command line shell by using psql handler

&nbsp;

~~~bash
psql -U username -d database -h localhost -p 5432
~~~

### or you can use this command if you are on ubuntu

&nbsp;

~~~bash
sudo -u postgres psql
~~~

### - Creating New User

Here is how you can create a new user in postgresql database:

~~~bash
CREATE USER Aliseyfi WITH PASSWORD 'aliseyfi@123';
~~~

### You can give your own username and password instead of "Aliseyfi" and "aliseyfi@123" password .

#### Note: postgres will make your username to lower case so for example if you give the username as "DAVID" it will be "david" at the end

&nbsp;

### -Creating New Database

Here is the database creation statement to run:

~~~bash
CREATE DATABASE Myapp;
~~~

#### Note: postgres will make your database name to lower case so for example if your database name is "TEST" it will be "test" at the end

&nbsp;

#### Note: we have two different part of commands in postgres

1 - SQL commands

2 - psql commands

&nbsp;

Now you can get the all databases list in your postgres server by running this psql command:

~~~bash
\l
~~~

### -Changing the owner of your database

Run this statement to change the owner of your database

(in this case and example my username is aliseyfi and my database name is myapp!)

~~~bash
ALTER DATABASE myapp OWNER TO aliseyfi;
~~~

### -Set all permissions for your database

Run this statement command to give all permissions to your new user about the new database you created.

~~~bash
GRANT ALL PRIVILEGES ON database myapp TO aliseyfi;
~~~

&nbsp;

## 3- Installing psycopg2 (Python-PostgreSQL Database Adapter)

You have to install the postgres client and interface ("psycopg2") for your django project.

Here is how you can install it by pip:

~~~bash
pip install psycopg2-binary
~~~

The binary package is a practical choice for development and testing

### Or  

You can install the psycopg2 itself that has external libraries and a compiler:

~~~bash
pip install psycopg2
~~~

&nbsp;

## 4- Set the PostgreSQL configurations in your settings.py django project

Replace this configuration with the django default sqlite3 configs in settings.py file in your project:

~~~python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'myapp',
        'USER': 'aliseyfi',
        'PASSWORD': 'aliseyfi@123',
        'HOST': '127.0.0.1',
        'PORT': '5432'
    }
}
~~~

### Note: you should give password of the new user you created as the value for the 'PASSWORD' Key at above settings

&nbsp;

## 5- migrate

Good job! Here is the last thing you have to do !!

~~~bash
python3 manage.py migrate
~~~

Here you are , now you have the PostgreSQL database in your django project and you can check it with psql commands so connect to postgres in your shell by using psql and run these psql commands:

+ list of your databases

~~~bash
\l
~~~

+ choosing your database

~~~bash
\c myapp
~~~

+ get the list of your database tables

~~~bash
\dt
~~~

# And Finished
