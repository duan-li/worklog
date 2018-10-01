---
layout: post
title: Laravel bind vs singleton
date: 2018-10-01 05:06 +0000
---
`Container::singleton` is the same as `Container::bind` with the third parameter set to `true`. [^1]

[^1]: [Laravel: Difference App::bind and App::singleton](https://stackoverflow.com/questions/25229064/laravel-difference-appbind-and-appsingleton)


```php
class MyClass
{
    public $value;
}


public function test_bind()
{
    $container = new Container();

    $container->bind(MyClass::class);

    $instance1 = $container->make(MyClass::class);
    $instance2 = $container->make(MyClass::class);

    static::assertNotSame($instance1, $instance2);
}

public function test_singleton()
{
    $container = new Container();

    $container->singleton(MyClass::class);

    $instance1 = $container->make(MyClass::class);
    $instance2 = $container->make(MyClass::class);

    static::assertSame($instance1, $instance2);
}

```

---
