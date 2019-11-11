---
layout: post
title: pyinstaller
date: 2019-11-08 03:33 +0000
---



## ubuntu

```bash
1  apt-get update
    2  apt-get install python3
    3  apt-get install python3 pip3 -y
    4  apt-get install python3 pip -y
    5  apt-get install python3
    6  apt-cache search pip
    7  apt-cache search python3-pip
    8  apt-get install python3-pip -y
    9  pip3 -v
   10  pip
   11  pip3 install pyinstaller
   12  ls
   13  cd py
   14  ls
   15  rm -Rf build dist
   16  ls -l
   17  rm -Rf __pycache__
   18  rm p.spec
   19  rm ppp.spec
   20  rm _p.spec
   21  ls -l
   22  pyinstaller ./p.py
   23  ls
   24  cd dist
   25  ls
   26  cd p
   27  ls
   28  ./p
   29  ls
   30  history
   31  pip3 install flask
   32  ls
   33  cd ..
   34  ls
   35  cd ..
   36  ls
   37  apt-get install nano -y
   38  nano web.py
   39  python web.py &
   40  python3 web.py &
   41  apt-get install wget -y
   42  wget http://127.0.0.1:5000/
   43  cat index.html
   44  curl
   45  apt-get install wget curl-y
   46  apt-get install wget curl -y
   47  ls
   48  curl http://127.0.0.1:5000/
   49  pyinstaller web.py
   50  ls
   51  cd dist/
   52  ls
   53  cd web
   54  ls
   55  ps -a
   56  kill 4349
   57  ls
   58  curl http://127.0.0.1:5000/
   59  ls
   60  ./web
   61  ./web &
   62  curl http://127.0.0.1:5000/
   63  history
```

## alpine linux


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