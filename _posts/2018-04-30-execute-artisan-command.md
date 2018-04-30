---
layout: post
title: Execute Artisan Command
date: 2018-04-30 21:57 +1000
---

```php
\Illuminate\Support\Facades\Artisan::call('command', [
    'param1' => 'value',
    '--param2' => 'value',
]);

```