---
layout: post
title: django
---

* Prepare
  * python venv 1.1
  * Poetry 1.2
* Django
  * Install Django 2.1


## 1.2 Poetry

Poetry is a dependency management and packaging tool for Python. It simplifies the process of managing dependencies and creating Python projects. This guide will show you how to install Poetry, create a new project, and manage dependencies.

### Install
Start by installing Poetry on your system. You can install it using pip, the Python package installer.

```bash
pip install poetry
```

### Create a new project
To create a new project, run the following command in your terminal.

```bash
poetry new myproject
```

### Project structure
This will create a new directory called myproject, with the following structure:

```bash
myproject
├── myproject
│   └── __init__.py
├── pyproject.toml
└── README.rst
```

The pyproject.toml file is the Poetry configuration file. It contains all the information required to manage your project dependencies.

### Activate the virtual environment

 Poetry creates a virtual environment for your project to manage dependencies.

```bash
poetry shell
```


### Add dependencies

Open the pyproject.toml file in the root of your project. This file contains the project metadata and the dependencies section. Add your project's dependencies under the [tool.poetry.dependencies] section. 

```yaml
[tool.poetry.dependencies]
python = "^3.10"
requests = "^2.26.0"
```

### Install dependencies

To install the dependencies, run the following command in your terminal.

```bash
poetry install
```


### Add package

```bash
poetry add requests
```

### Init project

```bash
poetry init myProject
```


### Run project
Poetry allows you to define scripts and commands that can be executed within your project. Open the pyproject.toml file and add your custom scripts under the [tool.poetry.scripts] section. For example:

```yaml
[tool.poetry.scripts]
hello = "myproject.main:hello"
```

```bash
poetry run hello
```


## 2.1 Install Django

Start by creating a new Django project. Navigate to the directory where you want to create your project and run the following command:

```bash

poetry init django myproject
```
But sometimes you may want to create a project in a directory that is not empty. Or get poetry error `No arguments expected for "init" command, got "django"`.

Run the following command to initialize a new Poetry project without add any dependencies.

```bash
# in your poetry project
poetry init
```

This command will prompt you to provide information about your project, such as name, version, author, and description. You can press Enter to accept the default values or provide your own.

Once the Poetry project is initialized, you can install Django as a dependency by running the following command.

```bash
poetry add django
```

## Create a Django project

To create a new Django project structure within your Poetry project, run the following command.

```bash
poetry run django-admin startproject myproject .
```

## Create a Django app

To create a new Django app within your Poetry project, run the following command.

```bash
poetry run python manage.py startapp myapp
```

## Different between project and app

A Django project is a collection of settings and apps that make up a Django site. A Django app is a Web application that does something – e.g., a Weblog system, a database of public records or a simple poll app. A project can contain multiple apps. An app can be in multiple projects.

## Verify Django installation

```bash
poetry run python manage.py runserver
```