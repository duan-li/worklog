---
layout: post
title: Disk usage statistics in linux
date: 2022-07-12 03:56 +0000
---

In Linux, you can use various commands and tools to obtain disk usage statistics, like `df` or `du`. 



## `df` command

The `df` command provides information about file system disk space usage on Linux systems. By default, it displays disk usage in kilobytes (KB), but you can specify different units if needed. Here's the basic usage:

```bash
df -h
```

## `du` command

`du` Command: The du command is used to estimate file and directory sizes. It recursively traverses directories and reports the disk usage of each file and directory. Here's an example of how to use it:

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
