---
layout: post
title: Phpunit test controller
date: 2018-02-15 14:06:03 +1000
---
Two ways to test method of controller

```php
$response = $this->get(action('Admin\RetailersController@edit', [$retailer->id]))
            ->assertSuccessful();
```

```php
$this->get(route("admin.offers.create"))
            ->assertSuccessful();
```