---
layout: post
title: Python localization
date: 2019-02-01 11:11 +0000
---


## Python and pip


```
apk --update add python3
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


### `requirements.txt` [^3]

Content of `requirements.txt` will like 
```
Django==2.1.5
pytz==2018.9
```


```
pip freeze > requirements.txt
pip install -r requirements.txt
pip install -r requirements.txt --target vendor
```

#### Example of requirements file [^4]
```bash
#
####### example-requirements.txt #######
#
###### Requirements without Version Specifiers ######
nose
nose-cov
beautifulsoup4
#
###### Requirements with Version Specifiers ######
#   See https://www.python.org/dev/peps/pep-0440/#version-specifiers
docopt == 0.6.1             # Version Matching. Must be version 0.6.1
keyring >= 4.1.1            # Minimum version 4.1.1
coverage != 3.5             # Version Exclusion. Anything except version 3.5
Mopidy-Dirble ~= 1.1        # Compatible release. Same as >= 1.1, == 1.*
#
###### Refer to other requirements files ######
-r other-requirements.txt
#
#
###### A particular file ######
./downloads/numpy-1.9.2-cp34-none-win32.whl
http://wxpython.org/Phoenix/snapshot-builds/wxPython_Phoenix-3.0.3.dev1820+49a8884-cp34-none-win_amd64.whl
#
###### Additional Requirements without Version Specifiers ######
#   Same as 1st section, just here to show that you can put things in any order.
rejected
green
#
```

[^1]: [Install a Python package into a different directory using pip?](https://stackoverflow.com/questions/2915471/install-a-python-package-into-a-different-directory-using-pip)

[^2]: [pip install options “no-cache-dir” and “target” don't work well together?](https://stackoverflow.com/questions/52267470/pip-install-options-no-cache-dir-and-target-dont-work-well-together)

[^3]: [pip 19.0.1 documentation » User Guide](https://pip.pypa.io/en/stable/user_guide/)

[^4]: [Example Requirements File](https://pip.pypa.io/en/stable/reference/pip_install/#example-requirements-file)

---