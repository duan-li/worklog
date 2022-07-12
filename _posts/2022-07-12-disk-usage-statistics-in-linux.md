---
layout: post
title: Disk usage statistics in linux
date: 2022-07-12 03:56 +0000
---

### Check single directory.

```bash
du -sh /var
```

### Check all elements in a path

```bash
du -shc /var/*
```

### Check all elements include one level sub-directory in a path

```bash
du -h --max-depth=1 /var
```

### Sort by size and list top 5

```bash
du -h /var/ | sort -rh | head -5
```


## Ref

- https://linuxize.com/post/how-get-size-of-file-directory-linux/
