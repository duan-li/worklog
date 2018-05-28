---
layout: post
title: Laravel project standards
date: 2018-05-08 15:23 +0000
---

## `\` for php function 
```
\isset($var);

```
 - [PHP - Global space](http://www.php.net/manual/en/language.namespaces.global.php)


## No `\Exception`
Should use customized exception class like 
```php
<?php
declare(strict_types=1);

class DriverException extends \Exception
{

}
```

This is because we can use `Handler` to filter different exceptions.

## The Repository Design Pattern
https://medium.com/@connorleech/use-the-repository-design-pattern-in-a-laravel-application-13f0b46a3dce
https://github.com/connor11528/laravel-vue-tasks
https://www.dunebook.com/brief-overview-of-design-patterns-used-in-laravel/3/
https://bosnadev.com/2015/03/07/using-repository-pattern-in-laravel-5/
http://www.laravelbestpractices.com/

## The Customize Request in controller
No `Illuminate\Http\Request` instance goes to any controller. 
Controller must use customize request class instance. 


## Test pattern
### Unit test (PoT)
Process-oriented test
For all task, unit test clearly show how function/program working. 

### Accessibility test (RoT)
Result-oriented test
For controller, Accessibility test doesn't know or care how function/program working.


## Decorating Laravel Repositories
https://matthewdaly.co.uk/blog/2017/03/01/decorating-laravel-repositories/