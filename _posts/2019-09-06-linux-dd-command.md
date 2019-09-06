---
layout: post
title: Linux dd command
date: 2019-09-06 16:42 +0000
---

## Creating an image file with dd command [^1]
[^1]: [Linux / UNIX: Create Large 1GB Binary Image File With dd Command](https://www.cyberciti.biz/faq/howto-create-lage-files-with-dd-command/)

First, make sure you've sufficient disk space to create a image file using dd:
```bash
$ df -H
```
To create 1MB file (1024kb), enter:
```bash
$ dd if=/dev/zero of=test.img bs=1024 count=0 seek=1024
```
You will get an empty files (also known as "sparse file") of arbitrary size using above syntax. To create 10MB file , enter:
```bash
$ dd if=/dev/zero of=test.img bs=1024 count=0 seek=$[1024*10]
```
To create 100MB file , enter:
```bash
$ dd if=/dev/zero of=test.img bs=1024 count=0 seek=$[1024*100]
$ ls -lh test.img
```

To create 500MB file , enter:
```bash
$ dd if=/dev/zero of=test.img bs=1024 count=0 seek=$[1024*500]
```

To create 1GB, file:
```bash
$ dd if=/dev/zero of=1g.img bs=1 count=0 seek=1G
```


---


