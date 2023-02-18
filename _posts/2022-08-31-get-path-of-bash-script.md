---
layout: post
title: Get path of bash script
date: 2022-08-31 11:24 +0000
categories: [System]
tags: [command line, bash]
---

Obtaining the path of a bash script can be useful in various scenarios.

1. Relative File Operations: If your script needs to read or write files relative to its own location, knowing the script path allows you to construct file paths correctly. For example, if your script includes additional resource files or configuration files located in the same directory, you can reference them using the script path as a base.
1. Logging and Debugging: When logging or debugging a bash script, including the script's path in the output can help identify the specific script that generated the log or error message. It aids in troubleshooting and understanding the context of the script's execution.
1. Including Other Scripts: If your script includes or sources other scripts located in the same directory, knowing the script path enables you to include them using a relative path. This helps maintain the portability of the script, as it can be moved to different locations without requiring modifications to the included script paths.
1. Configuration and Initialization: Some scripts may have configuration files or initialization routines located in the same directory. Obtaining the script path allows the script to locate and load these resources correctly during its execution.
1. Self-Referencing: In some cases, a script may need to refer to itself, for example, to restart or execute a new instance with specific arguments. Knowing the script path allows the script to reference itself accurately.


## How to obtain the location of a bash script

Here is an example depth-indented listing of files.

```bash
/
 |-/tmp
 |  |-foo
 |  |  |-bin
 |  |  |  |-script.sh
 |-/home
 |  |-mike
 |  |  |-bin
 |  |  |  |-script_link -> (symlink to /tmp/foo/bin/script.sh)
```

Here are three ways to obtain the path of a bash script.

### Script 1


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

### Script 2
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

### Script 3

What about if get path of script when wexecuted through a symlink. [^link]

[^link]: [Get path of current script when executed through a symlink](https://unix.stackexchange.com/questions/17499/get-path-of-current-script-when-executed-through-a-symlink)

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
