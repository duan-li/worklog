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




```php
/**
 * @link https://wiki.php.net/rfc/iterable
 */
interface iterable {}
```


```php
/**
 * Interface to detect if a class is traversable using &foreach;.
 * @link http://php.net/manual/en/class.traversable.php
 */
interface Traversable extends iterable {
}
```

```php
/**
 * Interface to create an external Iterator.
 * @link http://php.net/manual/en/class.iteratoraggregate.php
 */
interface IteratorAggregate extends Traversable {

    /**
     * Retrieve an external iterator
     * @link http://php.net/manual/en/iteratoraggregate.getiterator.php
     * @return Traversable An instance of an object implementing <b>Iterator</b> or
     * <b>Traversable</b>
     * @since 5.0.0
     */
    public function getIterator();
}
```

```php
/**
 * Interface for external iterators or objects that can be iterated
 * themselves internally.
 * @link http://php.net/manual/en/class.iterator.php
 */
interface Iterator extends Traversable {

    /**
     * Return the current element
     * @link http://php.net/manual/en/iterator.current.php
     * @return mixed Can return any type.
     * @since 5.0.0
     */
    public function current();

    /**
     * Move forward to next element
     * @link http://php.net/manual/en/iterator.next.php
     * @return void Any returned value is ignored.
     * @since 5.0.0
     */
    public function next();

    /**
     * Return the key of the current element
     * @link http://php.net/manual/en/iterator.key.php
     * @return mixed scalar on success, or null on failure.
     * @since 5.0.0
     */
    public function key();

    /**
     * Checks if current position is valid
     * @link http://php.net/manual/en/iterator.valid.php
     * @return boolean The return value will be casted to boolean and then evaluated.
     * Returns true on success or false on failure.
     * @since 5.0.0
     */
    public function valid();

    /**
     * Rewind the Iterator to the first element
     * @link http://php.net/manual/en/iterator.rewind.php
     * @return void Any returned value is ignored.
     * @since 5.0.0
     */
    public function rewind();
}
```

---