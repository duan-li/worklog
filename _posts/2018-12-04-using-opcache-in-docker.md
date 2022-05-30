---
layout: post
title: Using OPcache in Docker
date: 2018-12-04 21:59 +0000
---

## Opcache and JIT

* [What's the difference between the opcache of PHP and the latest PHP jit?](https://developpaper.com/question/whats-the-difference-between-the-opcache-of-php-and-the-latest-php-jit/)
* [Best Zend OpCache Settings / Tuning / Configurations](https://gist.github.com/rohankhudedev/1a9c0a3c7fb375f295f9fc11aeb116fe)
* [Exploring the New PHP JIT Compiler - Zend](https://www.zend.com/blog/exploring-new-php-jit-compiler)
* [PHP 8: How to setup the JIT](https://stitcher.io/blog/php-8-jit-setup)
* [Runtime Configuration - Official](https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.jit-buffer-size)


## Example Config on Container 


```bash
[opcache]
opcache.enable=1

; # 0 means it will check on every request
; # 0 is irrelevant if opcache.validate_timestamps=0 which is desirable in production
opcache.revalidate_freq=0

; # how often to check script timestamps for updates, in seconds. 
; # 0 will result in OPcache checking for updates on every request.
opcache.validate_timestamps=1

; # The maximum number of keys (and therefore scripts) in the OPcache hash table
opcache.max_accelerated_files=10000

; # The size of the shared memory storage used by OPcache, in megabytes.
opcache.memory_consumption=256

; # The maximum percentage of wasted memory that is allowed before a restart is scheduled.
opcache.max_wasted_percentage=10

; # The amount of memory used to store interned strings, in megabytes. 
opcache.interned_strings_buffer=16

; # If enabled, a fast shutdown sequence is used that doesn't free each allocated block, but relies on the Zend Engine memory manager to deallocate the entire set of request variables en masse.
; # Removed in PHP 7.2.0
opcache.fast_shutdown=1
```

The most important setting for development is the `opcache.validate_timestamps=1` which allows us to make changes to our code. If you’re using a Docker volume, it means that OPcache will respect file timestamps and your changes will reflect immediately. In a production environment that’s not ideal, and that’s where our dynamic configuration will come into play shortly.[^1]

[^1]: [Speeding Up PHP with OPcache in Docker](https://laravel-news.com/php-opcache-docker)






---