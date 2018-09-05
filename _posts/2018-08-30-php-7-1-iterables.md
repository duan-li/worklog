---
layout: post
title: PHP 7.1 Iterables
date: 2018-08-30 12:07 +0000
---

> Iterable is a pseudo-type introduced in PHP 7.1. 

It accepts any array or object implementing the Traversable interface. Both of these types are iterable using foreach and can be used with yield from within a generator. [^1]

[^1]: [PHP iterable type](http://php.net/manual/en/language.types.iterable.php)


```php
function foo(iterable $iterable = []) {
    foreach ($iterable as $value) {
        // ...
    } 
}
```

```php
function foo(): iterable {
    return [1, 2, 3];
}
```


> PHP allows you to specify the type of a function/method parameter or return value. These return values can be any legal PHP type, which includes any class or interface type, various scalars, and some fancy pseudo-types like `callable` and `iterable`. [^2]

[^2]: [PHP: Never type hint on arrays](https://steemit.com/php/@crell/php-never-type-hint-on-arrays)




---