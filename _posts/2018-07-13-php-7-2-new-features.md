---
layout: post
title: PHP 7.2 new features
date: 2018-07-13 05:43 +0000
---

## Parameter type change between parent class and child class
```php
class Parent{
	public function sum($numbers){}
}
 
class Child extends Parent{
	public function sum(array $numbers){}
}
```

## Parameter type change between parent abstract class 
```php
class Parent{
	public function sum($numbers){}
}
 
class Child extends Parent{
	public function sum(array $numbers){}
}

```
## Trailing comma in list syntax
## Object Type Hinting
## New Sodium extension
## Argon2 in password hash