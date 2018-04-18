---
layout: post
title: "[PHP]Creating instance of dynamic class"
date: 2018-04-18 15:50 +1000
---


```php
$classPath = \explode("\\", __NAMESPACE__);
\array_pop($classPath);
$newPath = \implode("\\", $classPath) . "\\Drivers\\";
$className = $newPath . Str::studly($this->driver);
if (!\class_exists($className)) {
    throw new DriverException('Could not find driver');
}


return new $className();
```