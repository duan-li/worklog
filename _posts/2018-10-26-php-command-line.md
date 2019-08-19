---
layout: post
title: PHP command line
date: 2018-10-26 00:25 +0000
---


## PHP Cli

* `php -i`: like phpinfo(); you can use `php -i | less` to show detail one by one.
* `php -f sample.php`: run php file in cli.
* `php -r`: run php code in cli, like `php -r "print_r('hi');"`
* `php -a`: Interactive shell for PHP [^1]

[^1]: [How to Use and Execute PHP Codes in Linux Command Line](https://www.tecmint.com/run-php-codes-from-linux-commandline/)


## PHP server

start php server `php -S localhost:8000 -t ./`

check php model `php -m | grep soap`

## Install xDebug via pecl

```
pecl install xdebug
```

### PHP 5.4

Pear error "XML Extension not found" [^2]

[^2]: [pear install xdebug](https://stackoverflow.com/questions/40999752/pear-error-xml-extension-not-found-on-ubuntu-14-04-after-installing-php-xml);

```bash
sed -i "$ s|\-n||g" /usr/bin/pecl
```

---




