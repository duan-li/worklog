---
layout: post
title: alpine install php5 redis
date: 2019-06-28 04:32 +0000
---



```bash
0 apk update
   1 apk search php
   2 apk search php5
   3 apk search php5-redis
   4 apk search redis
   5 apk add curl openssl php5-cli php5-dev php5-xml php5-dom php5-openssl
   6 apk add curl openssl php5-cli php5-dev php5-xml php5-dom php5-openssl pe
   7 apk search pecl
   8 apk add curl openssl php5-cli php5-dev php5-xml php5-dom php5-openssl php5-pear
   9 pecl
  10 php5
  11 php
  12 /usr/bin/php5
  13 ln -s /usr/bin/php5 /usr/bin/php
  14 php
  15 ln -s /usr/bin/phpize5 /usr/bin/phpize
  16 pecl
  17 peclpecl install -o -f redis
  18 pecl install -o -f redis
  19 curl
  20 apk search autoconf
  21 apk insatll autoconf
  22 apk add autoconf
  23 pecl install -o -f redis
  24 history
  25 ls
  26 apk add c
  27 apk add gcc
  28 pecl install -o -f redis
  29 apk search libc
  30 apk search libc6
  31 apk add libc6-compat
  32 pecl install -o -f redis
  33 apk add libc6
  34 apk add libc6-dev
  35 apk add libc-dev
  36 pecl install -o -f redis
  37 apk add make
  38 pecl install -o -f redis
  39 cd /etc/php5/
  40 cd conf.d/
  41 ls
  42 echo "extension=redis.so" > redis.ini
  43 ls
  44 cat redis.ini
  45 cat xml.ini
  46 pecl search yaml
  47 pecl install -o -f yaml
  48 history
```


```bash
apk add --update curl openssl php5-cli php5-dev php5-xml php5-dom php5-openssl php5-pear autoconf gcc make libc6-compat libc-dev 
ln -s /usr/bin/php5 /usr/bin/php
ln -s /usr/bin/phpize5 /usr/bin/phpize
printf "\n" | pecl install -o -f redis
echo "extension=redis.so" > /etc/php5/conf.d/redis.ini
```




---