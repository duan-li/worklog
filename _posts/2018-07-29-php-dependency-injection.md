---
layout: post
title: PHP Dependency Injection
date: 2018-07-29 18:41 +0000
---

> Keyword: PHP-DI, PSR-11, Autowriing

Dependency injection allow you inject an object into another object[^1].

> Dependency Injection Container is the way to manage injecting and reading objects and third party libraries in your application.

PHP-FIG PSR-11[^2] is a standard guide you to implement container.

```php
interface ContainerInterface {
    public function get($id);
    public function has($id);
}
```


## Example

```php
class Wheel
{

}

class Car
{
    private $wheel;

    public function __construct(Wheel $wheel)
   {
      $this->wheel = $wheel;
   }
}


$wheel = new Wheel;

$car = new Car($wheel);
```
At above example, every new `Car` object need `Wheel` object. That is dependency.
new `Car` object is dependent on `Wheel` object.


As we can see, PSR-11 define two method `has` and `get`. `get` method will resolve dependency by using `Reflection`[^3]. It provides autowiring[^4].

PHP has native `Reflection`[^7].



Want study more about dependency injection, check out PHP-DI[^5].

There is also another example demo a very simple container[^6].

[^1]: [Dependency Injection (DI) Container in PHP](https://medium.com/tech-tajawal/dependency-injection-di-container-in-php-a7e5d309ccc6)
[^2]: [PHP-FIG PSR-11](https://www.php-fig.org/psr/psr-11/)
[^3]: [Introduction to PHP Reflection API](https://medium.com/tech-tajawal/introduction-to-php-reflection-api-4af07cc17db4)
[^4]: [Autowiring](https://symfony.com/doc/current/service_container/autowiring.html)
[^5]: [PHP-DI](http://php-di.org/)
[^6]: [PHP Dependency Injection Container](https://gist.github.com/tlikai/6086973)
[^7]: [PHP reflection](http://php.net/manual/en/book.reflection.php)

---
