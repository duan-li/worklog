---
layout: post
title: Nginx+PHP docker compose
date: 2018-05-13 20:42 +0000
---


```
location ~ \.php$ {
    	proxy_intercept_errors on;
        fastcgi_keep_conn on;
		client_max_body_size 1024M;
        try_files      $uri =404;

        include        /etc/nginx/fastcgi_params;
        fastcgi_param   SCRIPT_FILENAME         $document_root$fastcgi_script_name;
		fastcgi_pass unix:/run/php/php7.0-fpm.sock;
        fastcgi_index  index.php;
		fastcgi_read_timeout 120;
    }
```

```
docker run -it \
-v /root/php/php7:/etc/php7:ro \
-v /root/php/www:/var/www \
-v /root/php/run:/run/php \
-v /root/php/log:/var/log/php7 \
-p 9000:9000 php

docker run -it \
-v /root/nginx-php/php/php7:/etc/php7:ro \
-v /root/nginx-php/php/www:/var/www \
-v /root/nginx-php/php/run:/run/php \
-v /root/nginx-php/php/log:/var/log/php7 dockercraft/php:php-fpm-7.1


docker run -it \
-v /Users/DHome/Dockercraft/nginx/nginx:/etc/nginx:ro \
-v /Users/DHome/Dockercraft/nginx/log:/var/log/nginx \
-v /Users/DHome/Dockercraft/nginx/run:/run/nginx \
-v /Users/DHome/Dockercraft/nginx/www:/var/www \
-p 8090:80 nginx

```




```
version: '2'
services:

  php:
    image: dockercraft/php:php-fpm-7.1
    container_name: php-fpm
    volumes:
      - ./php/php7:/etc/php7:ro
      - ./www:/var/www:rw
      - ./php/run:/run/php:rw
      - ./php/log:/var/log/php7:rw

  nginx:
    image: dockercraft/nginx:latest
    depends_on:
      - php
    container_name: nginx
    volumes:
      - ./nginx/nginx:/etc/nginx:ro
      - ./nginx/log:/var/log/nginx
      - ./nginx/run:/run/nginx
      - ./php/run:/run/php
      - ./www:/var/www
    restart: on-failure
    ports:
      - "80:80"

```
