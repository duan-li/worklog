---
layout: post
title: PHP 7.4 new features
date: 2020-05-25 00:04 +0000
---

## New feature

### [Arrow functions](https://wiki.php.net/rfc/arrow_functions_v2)

```php
array_map(function (User $user) { 
    return $user->id; 
}, $users)
```

You can now write this:

```php
array_map(fn (User $user) => $user->id, $users)
```

* They can always access the parent scope, there's no need for the `use` keyword.
* `$this` is available just like normal closures.
* Arrow functions may only contain one expression, which is also the return statement.


### Typed properties

```php
class A
{
    public string $name;
    
    public ?Foo $foo;
}

```

### [Improved type variance](https://wiki.php.net/rfc/covariant-returns-and-contravariant-parameters)

```php
class ParentType {}
class ChildType extends ParentType {}

class A
{
    public function covariantReturnTypes(): ParentType
    { /* … */ }
}

class B extends A
{
    public function covariantReturnTypes(): ChildType
    { /* … */ }
}
```


```php 

class A
{
    public function contraVariantArguments(ChildType $type)
    { /* … */ }
}

class B extends A
{
    public function contraVariantArguments(ParentType $type)
    { /* … */ }
}

```


### Null coalescing assignment operator

```php
$data['date'] = $data['date'] ?? new DateTime();
```

You can do this:

```php
$data['date'] ??= new DateTime();
```


### Array spread operator

```php
$arrayA = [1, 2, 3];

$arrayB = [4, 5];

$result = [0, ...$arrayA, ...$arrayB, 6 ,7];

// [0, 1, 2, 3, 4, 5, 6, 7]
```


### Numeric Literal Separator

```php
$unformattedNumber = 107925284.88;

$formattedNumber = 107_925_284.88;

```


### [Foreign function interface](https://wiki.php.net/rfc/ffi)

```php
// create FFI object, loading libc and exporting function printf()
$ffi = FFI::cdef(
    "int printf(const char *format, ...);", // this is regular C declaration
    "libc.so.6");
// call C printf()
$ffi->printf("Hello %s!\n", "world");

```

### [Preloading](https://wiki.php.net/rfc/preload)

Preloading is going to be controlled by just a single new php.ini directive - opcache.preload. Using this directive we will specify a single PHP file - which will perform the preloading task. Once loaded, this file is then fully executed - and may preload other files, either by including them or by using the opcache_compile_file() function. Previously, I tried to implement a rich DSL to specify which files to load, which to ignore, using pattern matching etc, but then realized that writing the preloading scenarios in PHP itself was much more simple and much more flexible.

### [Custom object serialization](https://wiki.php.net/rfc/custom_object_serialization)

Two new magic methods have been added: `__serialize` and `__unserialize`. The difference between these methods and `__sleep` and `__wakeup` is discussed in the RFC.

```php
public function serialize() {
    return serialize([$this->prop1, $this->prop2]);
}
```


### [Reflection for references](https://wiki.php.net/rfc/reference_reflection) 

Libraries like Symfony's var dumper rely heavily on the reflection API to reliably dump a variable. Previously it wasn't possible to properly reflect references, resulting in these libraries relying on hacks to detect them.

PHP 7.4 adds the `ReflectionReference` class which solves this issue.



### [Changes and deprecations](https://wiki.php.net/rfc/weakrefs)

Weak references are references to objects, which don't prevent them from being destroyed.

### `mb_str_split`

This function provides the same functionality as `str_split`, but on multi-byte strings.


### [Password Hashing Registry](https://wiki.php.net/rfc/password_registry)

Internal changes have been made to how hashing libraries are used, so that it's easier for userland to use them.

More specifically, a new function `password_algos` has been added which returns a list of all registered password algorithms.


## Changes and deprecations


### [Left-associative ternary operator deprecation](https://wiki.php.net/rfc/ternary_associativity)

```php
1 ? 2 : 3 ? 4 : 5;   // deprecated
(1 ? 2 : 3) ? 4 : 5; // ok
```


### Exceptions allowed in `__toString`

https://wiki.php.net/rfc/tostring_exceptions

### [Concatenation precedence](https://wiki.php.net/rfc/concatenation_precedence)

If you'd write something like this:

```php
echo "sum: " . $a + $b;
```

PHP would previously interpret it like this:

```php
echo ("sum: " . $a) + $b;
```

PHP 8 will make it so that it's interpreted like this:

```php
echo "sum: " . ($a + $b);
```

PHP 7.4 adds a deprecation warning when encountering an unparenthesized expression containing a . before a `+` or `-` sign.






**Ref**

- https://stitcher.io/blog/new-in-php-74


