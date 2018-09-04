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



---