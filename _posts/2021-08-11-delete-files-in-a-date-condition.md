---
layout: post
title: Delete files in a date condition
date: 2021-08-11 12:16 +0000
---

Delete files before 1st of previous month.

```bash
#!/bin/sh

dir_to_check='/root/temp/somedir'

last_month=$(date -d "-1 month -$(($(date +%d)-1)) days" +%Y-%m-%d)

find "$dir_to_check" ! -newermt "$last_month" -type f -exec rm {} \;
```


```bash

find <dir> -type f -mtime +31 -exec rm {} \;

```