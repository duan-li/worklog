---
layout: post
title: Join query in laravel eloquent
date: 2018-09-04 00:23 +0000
---

```php
$posts = App\Post::whereHas('comments', function ($query) {
    $query->where('content', 'like', 'foo%');
})->get();
```

[^1]: [Querying Relationship Existence](https://laravel.com/docs/5.6/eloquent-relationships#querying-relationship-existence)