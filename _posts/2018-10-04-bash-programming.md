---
layout: post
title: Bash programming
date: 2018-10-04 13:15 +0000
---


File header

```bash
#!/bin/bash
```

CLI param

```bash
echo $1
echo $2
# cli param1 param2
```

Check param is (not) empty

```bash
if [ -z "$1" ]; then
    echo "empty param"
fi

if [ ! -z "$1" ]; then
    echo "not empty param"
fi
```

Put value to dynamiclly varable 

```
A_VAR='a'
eval "$1_VAR"='cc'
echo $A_VAR
```






