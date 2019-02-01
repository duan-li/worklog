---
layout: post
title: Python localization
date: 2019-02-01 11:11 +0000
---


## Python and pip


```
apk add python3
pip3 install --upgrade pip
pip -V
```

## Django

`pip install django==2.1.5`

### Create project

`django-admin startproject <project-directory>`


### Create app
goto `<project-directory>`

`python3 manage.py startapp <app-name>`




## tips

### Install django to local directory [^1]

`pip install --target <dir> package_name`

`pip install --target vendor django==2.1.5`

Make `PYTHONPATH` [^2]

```bash
export PYTHONPATH=/project/vendor
# or 
export PYTHONPATH=$PYTHONPATH:/project/vendor
```

`python3 vendor/bin/django-admin`




[^1]: [Install a Python package into a different directory using pip?](https://stackoverflow.com/questions/2915471/install-a-python-package-into-a-different-directory-using-pip)

[^2]: [pip install options “no-cache-dir” and “target” don't work well together?](https://stackoverflow.com/questions/52267470/pip-install-options-no-cache-dir-and-target-dont-work-well-together)

---