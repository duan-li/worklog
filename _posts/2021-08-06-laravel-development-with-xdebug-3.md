---
layout: post
title: Laravel development with xdebug 3
date: 2021-08-06 06:01 +0000
---


## Development env background

Laravel 8.x based on php 7.4 + xdebug 3.0.3 fpm with nginx, running in docker container. PHPstrorm as IDE.


## `php.ini` config


```ini
[xdebug]
;;;;; xdebug 3.0.3
zend_extension=xdebug.so
xdebug.mode=debug
xdebug.idekey=PHPSTORM
xdebug.remote_handler=dbgp

; xdebug 2 remote_autostart setting has been removed. Instead, set start_with_request in xdebug 3
xdebug.start_with_request=yes

; xdebug 2 remote_connect_back replaced by discover_client_host in xdebug 3
xdebug.discover_client_host=1

; xdebug 2 remote_port replaced by client_port in xdebug 3
xdebug.client_port=9003

; xdebug 2 remote_log_level replaced by log_level in xdebug 3
xdebug.log_level = 0

; windows or mac using host.docker.internal, linux using 127.0.0.1
xdebug.client_host=host.docker.internal

```


## Tips

Use `xdebug_info()` rather than `php_info()`, in order to diagnose why xdebug not working.;

```php
<?php

xdebug_info();

```

- [Upgrading from Xdebug 2 to 3](https://xdebug.org/docs/upgrade_guide)
- [Disable Xdebug 3 “Could not connect” message in CLI](https://stackoverflow.com/questions/65213171/disable-xdebug-3-could-not-connect-message-in-cli)
- [Xdebug: [Step Debug] Could not connect to debugging client](https://stackoverflow.com/questions/64878376/xdebug-step-debug-could-not-connect-to-debugging-client)
- [Docker + Xdebug + VSCode Could not connect to client](https://stackoverflow.com/questions/56099086/docker-xdebug-vscode-could-not-connect-to-client)
- [Xdebug Could not connect to debugging client. Tried: localhost:9000](https://stackoverflow.com/questions/65059303/xdebug-could-not-connect-to-debugging-client-tried-localhost9000)