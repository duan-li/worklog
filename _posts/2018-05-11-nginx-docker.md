---
layout: post
title: Nginx docker
date: 2018-05-11 22:05 +0000
---

`/Users/DHome/Dockercraft/nginx/ningx`

```
docker run -it \
-v /Users/DHome/Dockercraft/nginx/nginx:/etc/nginx:ro \
-v /Users/DHome/Dockercraft/nginx/log:/var/log/nginx \
-v /Users/DHome/Dockercraft/nginx/run:/run/nginx \
-v /Users/DHome/Dockercraft/nginx/www:/var/www \
-p 8090:80 nginx
```


https://github.com/nginxinc/docker-nginx
https://github.com/docker-library/docs/tree/master/nginx
https://gist.github.com/xameeramir/a5cb675fb6a6a64098365e89a239541d
