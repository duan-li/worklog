---
layout: post
title: Global space
date:   2018-02-13 11:06:03 +1000
categories: [Code]
tags: [PHP]
---

In PHP, the global space refers to the highest level of the PHP namespace hierarchy. It is also known as the global scope or global namespace. When you define variables, functions, classes, or constants outside of any namespaces, they are considered to be part of the global space.


> Without any namespace definition, all class and function definitions are placed into the global space - as it was in PHP before namespaces were supported. Prefixing a name with \ will specify that the name is required from the global space even in the context of the namespace.

Here's an example to illustrate the global space in PHP:

```php
<?php
namespace A\B\C;

/* This function is A\B\C\fopen */
function fopen() { 
     /* ... */
     $f = \fopen(...); // call global fopen
     return $f;
} 
```

In the above example, `$globalVariable`, `globalFunction()`, `GlobalClass`, and `GLOBAL_CONSTANT` are all defined in the global space. They can be accessed and used from anywhere within your PHP code.

However, it is generally considered good practice to minimize the use of variables and functions in the global space to avoid naming conflicts and improve code organization. It's recommended to encapsulate your code within appropriate namespaces or classes to provide better structure and modularity.


[PHP - Global space](http://www.php.net/manual/en/language.namespaces.global.php)