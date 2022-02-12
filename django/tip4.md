---
layout: default
title: Django Fullstack Tips
description: A knowledge-sharing platform
---

# Working with environment variables in your Django application

_Varun Sharma_
_Feb 11, 2022_

### What are environment variables?

Environment variables can be considered as dynamically set variables that exist in our execution environment as long as our environment runs. These are key-value stores of data that hold specific pieces of information.

### Why use environment variables?

Environment variable are used whenever we want to hide specific pieces of information from our code into the environment. This is usually done to hide sensitive information or to configure our application. The type of information can range from secret keys and passwords to database configurations. This hiding of information helps in keeping our codebase secure from any misuse. This also results in better maintenance of our code by not having to touch our code base in case of a change in values.

**Now that we have a basic understanding of what environment variables are and why they are useful, lets see how we can include it in our django project.**

There are many popular packages we can use to work with env files like but here we will use a package called [python-dotenv](https://www.example.com).

After you have created your django project, install the python-dotenv package using the following command:

`pip install python-dotenv`

After it has finished installing we can begin using it in our code. Let us say we want to use it in our settings.py file in our project and store information regarding our secret key and our database configuration.

The steps we are going to follow are:

1. Create a file that holds our environment variables.
2. import the package in the file where we want to use these variables.
3. Load the environment variables in our project's environment.
4. Use the variables in our python file to hide sensitive and configuration information.

So let us begin:

### Create a file that holds our environment variables

Our environment variables usually go in a file that is named **.env** by convention. We can place this inside our project folder. Inside it we can store our information like:
`

```
SECRET_KEY='django-insecure-m++w@7nbp09f%6xn^+qk1x2-iqrfa$j0g=3&@0tpshp3^!f89('

# Database settings

DATABASE_ENGINE='django.db.backends.postgresql'
DATABASE_NAME='simple_db'
DATABSE_USERNAME='jon_doe'
DATABASE_PASSWORD='mindfire'
```

### Import the python-dotenv package in the settings.py file

The next step is to import the package and its function in our settings.py file like:

`from dotenv import load_dotenv`

load_env is responsible for loading our variables. Additionally we also import the **os** to fetch the environment variable from the environment later.

### Load the environment variables in our project environment

Next, we load the environment variables in our project. We do so by using the following code:
`load_dotenv()`

That's it. All we have to do is call **load_env()** at the top after we import it from the package. This will load the values from our **.env** file we created earlier. What's left is to use them in our code.

### Use the variables

We can use these variables using the **getenv()** function of the **os** module in python as:

```
SECRET_KEY = os.getenv('SECRET_KEY')
DATABASES = {
    'default': {
        'ENGINE': os.getenv('DATABASE_ENGINE'),
        'NAME': os.getenv('DATABASE_NAME'),
        'USER': os.getenv('DATABSE_USERNAME'),
        'PASSWORD': os.getenv('DATABASE_PASSWORD'),
    }
}
```

That is it. Now if we run our django application, it would work as intended. Be sure to include it in your **.gitignore** files because we do not want to push this to our repositories online.

Official docs for [python-dotenv](https://www.example.com)

[back](../)
