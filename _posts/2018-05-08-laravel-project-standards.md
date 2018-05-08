---
layout: post
title: Laravel project standards
date: 2018-05-08 15:23 +0000
---

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

