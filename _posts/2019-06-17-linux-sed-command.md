---
layout: post
title: Linux sed command
date: 2019-06-17 00:23 +0000
---

`sed` is a Unix utility that parses and transforms text, using a simple, compact programming language. sed was developed from 1973 to 1974 by Lee E. McMahon of Bell Labs, and is available today for most operating systems. [^1]

[^1]: [Wikipedia](https://en.wikipedia.org/wiki/Sed)


To remove the line and print the output to standard out: [^2]

[^2]: [Delete lines in a text file that contain a specific string](https://stackoverflow.com/questions/5410757/delete-lines-in-a-text-file-that-contain-a-specific-string)
```bash
sed '/pattern to match/d' ./infile
```

To directly modify the file:
```bash
sed -i '/pattern to match/d' ./infile
```
To directly modify the file (and create a backup):
```bash
sed -i.bak '/pattern to match/d' ./infile
```
For Mac OS X and FreeBSD users:
```bash
sed -i '' '/pattern/d' ./infile
```




---