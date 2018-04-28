---
layout: post
title: "[PHP]Calling dynamic method by name"
date: 2018-04-23 09:42 +1000
---

```php

if (method_exists($this, $method)) {
    return $this->$method($data);
} else {
    throw new EntityException('Not found method');
}

```
