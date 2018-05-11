---
layout: post
title: PHP docker
date: 2018-05-08 17:07 +0000
---



```
FROM dockercraft/alpine:3.7
MAINTAINER Daniel <daniel@topdevbox.com>

# How-To
 # Local Build: docker build -t php .
 # Local Run: docker run -it php php-fpm -v

# trust this project public key to trust the packages.
ADD https://php.codecasts.rocks/php-alpine.rsa.pub /etc/apk/keys/php-alpine.rsa.pub


# make sure you can use HTTPS
RUN apk --update add ca-certificates

# add the repository, make sure you replace the correct versions if you want.
RUN echo "@php https://php.codecasts.rocks/v3.7/php-7.1" >> /etc/apk/repositories

RUN apk add --update php-fpm@php \
		php-common@php \
		php-curl@php \
		php-gd@php \
		php-mysqlnd@php \
		php-imap@php \
		php-pdo_mysql@php \
		php-xml@php \
		php7-mcrypt@php \
		php-mbstring@php \
		php-bcmath@php \
		&& rm -rf /var/cache/apk/*


EXPOSE 9000-9010

STOPSIGNAL SIGTERM

ENTRYPOINT ["/usr/sbin/php-fpm7", "-F"]

```

```
/usr/sbin # ./php-fpm7 -v
PHP 7.1.16 (fpm-fcgi) (built: Apr  9 2018 10:23:39)
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.1.0, Copyright (c) 1998-2018 Zend Technologies
```

https://github.com/dylanlindgren/docker-phpfpm/blob/master/Dockerfile

https://github.com/codecasts/php-alpine