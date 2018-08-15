---
layout: post
title: Python tracebacks
date: 2018-08-14 09:35 +0000
---

Common traceback errors:[^1]

* SyntaxError
* ImportError or ModuleNotFoundError
* AttributeError
* NameError


### SyntaxError

```python
>>> print('This is a test)

SyntaxError: EOL while scanning string literal
```


```python
File "syn.py", line 1
  def func
           ^
SyntaxError: invalid syntax
```


### ImportError or ModuleNotFoundError
```python
>>> import some
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ImportError: No module named some
```


### AttributeError
```python
>>> my_string = 'Python'  
>>> my_string.up()  
Traceback (most recent call last):
  File "<pyshell#8>", line 1, in <module>
    my_string.up()
AttributeError: 'str' object has no attribute 'up'
```

### NameError
```python
>>> print(var)
Traceback (most recent call last):
  File "<pyshell#10>", line 1, in <module>
    print(var)
NameError: name 'var' is not defined
```


[^1]: [Understanding Tracebacks in Python](https://dzone.com/articles/understanding-tracebacks-in-python)

---