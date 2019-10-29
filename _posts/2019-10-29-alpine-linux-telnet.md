---
layout: post
title: Alpine linux telnet
date: 2019-10-29 00:15 +0000
---

Install `busybox-extras` [^be]

[^be]: [How to install telnet into a alpine docker container. This is useful when using the celery remote debugger in a dev environment.](https://gist.github.com/Ryanb58/9e63e186981090d4f2de8ec0ea420e1d)

```bash
apk update
apk add busybox-extras
busybox-extras telnet localhost 6900
```

---