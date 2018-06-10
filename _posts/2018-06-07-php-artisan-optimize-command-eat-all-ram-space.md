---
layout: post
title: php artisan optimize command eat all ram space
date: 2018-06-07 11:26 +0000
---

## Solution 1
Working try first command, not use second one
```
composer update --no-scripts
composer dump-autoload -o
```

## Solution 2
Not trid yet
```
composer dumpautoload
composer update
```


Ref
* https://github.com/laravel/framework/issues/18383
* https://laracasts.com/discuss/channels/general-discussion/composer-update-script-php-artisan-clear-compiled-handling-the-pre-update-cmd-event-returned-with-an-error?page=2