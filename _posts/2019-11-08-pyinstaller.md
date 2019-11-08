---
layout: post
title: pyinstaller
date: 2019-11-08 03:33 +0000
---


```bash

  0 ls
   1 apk add --update python3
   2 pip3 install pyinstaller
   3 cd py
   4 ls
   5 pyinstaller ./p.py --name ppp
   6 ls
   7 pyinstaller ./p.py --onefile --name ppp
   8 apk search objcopy
   9 apk add binutils
  10 pyinstaller ./p.py --onefile --name ppp
  11 ls
  12 cd dist
  13 ls
  14 ./ppp
  15 cd ppp
  16 ls
  17 cd ..
  18 ls
  19 apk add libc-dev
  20 cd dist
  21 ls
  22 ./ppp
  23 sh ./ppp
  24 cat ppp
  25 apk add musl-dev
  26 apk add musl
  27 ls
  28 ./ppp
  29 cd /lib
  30 ls
  31 history
  
```