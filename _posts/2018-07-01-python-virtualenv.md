---
layout: post
title: python virtualenv
date: 2018-07-01 06:31 +0000
---

## pyvenv vs virtualenv [^vs1]

[^vs1]: [pyvenv vs virtualenv](https://www.reddit.com/r/learnpython/comments/4hsudz/pyvenv_vs_virtualenv/)

```bash
# Python3:
$ python -m venv myapp
# Python 2
$ virtualenv myapp
```


## Recommendation for beginners: [^recommendation]
This is my personal recommendation for beginners: start by learning virtualenv and pip, tools which work with both Python 2 and 3 and in a variety of situations, and pick up the other tools once you start needing them. 

[^recommendation]: [What is the difference between venv, pyvenv, pyenv, virtualenv, virtualenvwrapper, pipenv, etc?](https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe)




## ref
* [user guide](https://virtualenv.pypa.io/en/stable/userguide/)
* [windows+vagrant](https://github.com/gratipay/gratipay.com/issues/2327)
* [venv](https://docs.python.org/3/library/venv.html)

---