---
layout: post
title: Get path of bash script
date: 2022-08-31 11:24 +0000
---




Example depth-indented listing of files

```bash
/
 |-/tmp
 |  |-foo
 |  |  |-bin
 |  |  |  |-script.sh
 |-/home
 |  |-mike
 |  |  |-bin
 |  |-script_link -> (symlink to /tmp/foo/bin/script.sh)
```

## Script 1


```bash
#!/usr/bin/env bash
# content of /tmp/foo/bin/script.sh
BASE_PATH="$( cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null && pwd )"
echo $BASH_PATH
```

Get script path by execute `/tmp/foo/bin/script.sh`
```bash
$ /tmp/foo/bin/script.sh
/tmp/foo/bin # script directoery

$ /home/mike/bin/script_link
/home/mike/bin # link directory
```

## Script 2
Get path of current script when executed through a symlink
```bash
#!/usr/bin/env bash
# content of /tmp/foo/bin/script.sh
BASE_PATH="$(dirname "$(readlink "$0")")"
echo $BASH_PATH
```


```bash
$ /tmp/foo/bin/script.sh
. # current directory

$ /home/mike/bin/script_link
/tmp/foo/bin # script directory
```

## Script 3

```bash
#!/usr/bin/env bash
# content of /tmp/foo/bin/script.sh
BASE_PATH="$( cd "$( dirname $(readlink "${BASH_SOURCE[0]}") )" >/dev/null && pwd )"
echo $BASH_PATH
```

```bash
$ /tmp/foo/bin/script.sh
/tmp/foo/bin # script directory

$ /home/mike/bin/script_link
/tmp/foo/bin # script directory
```








