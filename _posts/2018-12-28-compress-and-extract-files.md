---
layout: post
title: Compress and extract files
date: 2018-12-28 10:47 +0000
---

## Command line

### File to `.tar`
```bash
tar -cvf file.tar filename
tar -cvf file.tar file1 file2
```

### Files to `.tar.gz`

`tar -cvf - inputfile1 inputfile2 | gzip > file.tar.gz`

### Folder to `.tar`

`tar -cvf name-of-archive.tar /path/to/directory-or-file`

### Folder to `.tar.gz`

`tar -czvf file.tar.gz /dir`

### Folder to `.tar.bz2`

`tar -cjvf file.tar.bz2 /dir`

### `.tar` to `.tar.gz`

`gzip file.tar`


### `.tar.gz` to folder

```bash
tar -xzvf file.tar.gz
tar -xzvf file.tar.gz -C /dir
```


## Flags

Flag | Description
------------ | -------------
`-c` | Create an archive.
`-z` | Compress the archive with gzip.
`-v` |  Display progress in the terminal while creating the archive, also known as “verbose” mode. The v is always optional in these commands, but it’s helpful.
`-f` | Allows you to specify the filename of the archive.


---
