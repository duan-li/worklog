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