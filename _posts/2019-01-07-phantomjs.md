---
layout: post
title: PhantomJS
date: 2019-01-07 15:45 +0000
---

## centos 7
```
yum install epel-release -y
yum install nodejs npm bzip2 fontconfig -y

npm install -g phantomjs-prebuilt -unsafe-perm

```

## alpine linux [^1]

[^1]: https://github.com/Overbryd/docker-phantomjs-alpine/releases/tag/2.11

```bash
apk update && apk add --no-cache curl tar fontconfig && \
  mkdir -p /usr/share && \
  cd /usr/share \
  && curl -L https://github.com/Overbryd/docker-phantomjs-alpine/releases/download/2.11/phantomjs-alpine-x86_64.tar.bz2 | tar xj \
  && ln -s /usr/share/phantomjs/phantomjs /usr/bin/phantomjs \
  && phantomjs --version

```

---