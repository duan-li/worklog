---
layout: post
title: python virtualenv
date: 2018-07-01 06:31 +0000
tags : [python, virtualenv]
categories: [Development]
---

A virtual environment is a self-contained Python environment that allows you to isolate Python packages and dependencies for different projects. It provides a way to create a separate environment with its own installed packages, Python interpreter, and configuration settings, independent of the system-wide Python installation.

Virtual environments in Python provide a structured and controlled environment for Python projects, allowing for better dependency management, reproducibility, flexibility, and security. They are considered a best practice in Python development and are widely used by developers to ensure clean and isolated project environments.


## Get started

To create and use virtual environments in Python. You will need ensure that you have Python installed on your system. You can check the version of Python installed on your system by running the following command in your terminal.

### Install
Pip is the default package manager for Python, used for installing and managing Python packages. It is usually bundled with Python installations.

```bash
pip install virtualenv
```

### Create a virtual environment

Run the following command to create a new virtual environment.

```bash
# macos, python3
python3 -m venv myenv

# windows, python3
python -m venv myenv

# python2
virtualenv myapp
```


### Activate
Activate the virtual environment using the appropriate command for your operating system
```bash
source myenv/bin/activate

# windows
myenv\Scripts\activate.bat

```


### Deactivate 

To exit the virtual environment and return to your system's default Python environment, run the following command

```bash
deactivate
```

Using a virtual environment is a best practice for isolating Python projects and managing their dependencies separately. It allows you to avoid conflicts between different project dependencies and provides a clean and consistent environment for your Python development.

## Recommendation for beginners: [^recommendation]
This is my personal recommendation for beginners: start by learning virtualenv and pip, tools which work with both Python 2 and 3 and in a variety of situations, and pick up the other tools once you start needing them. 

[^recommendation]: [What is the difference between venv, pyvenv, pyenv, virtualenv, virtualenvwrapper, pipenv, etc?](https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe)


## Others

### pyvenv

`pyvenv` was a virtual environment tool introduced in Python 3.3 but is now deprecated in favor of the venv module. It is recommended to use venv for creating virtual environments in Python 3.3 and newer versions.


#### pyvenv vs virtualenv [^vs1]

[^vs1]: [pyvenv vs virtualenv](https://www.reddit.com/r/learnpython/comments/4hsudz/pyvenv_vs_virtualenv/)



## virtualenv

`virtualenv` has been a popular choice for managing virtual environments, it's important to note that starting from Python 3.3, the built-in `venv` module was introduced as a standard tool for creating virtual environments. It is recommended to use `venv` for creating virtual environments in Python 3.3 and newer versions, as it provides similar functionality to `virtualenv` without the need for an additional installation.

```bash
virtualenv project-name # create new project
# or 
virtualenv . # initial exist project

source project-name/bin/activate
```


## ref
* [user guide](https://virtualenv.pypa.io/en/stable/userguide/)
* [windows+vagrant](https://github.com/gratipay/gratipay.com/issues/2327)
* [venv](https://docs.python.org/3/library/venv.html)

---