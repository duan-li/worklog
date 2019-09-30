---
layout: post
title: Bash programming
date: 2018-10-04 13:15 +0000
---


## File header

```bash
#!/bin/bash
```

## CLI param

```bash
echo $1
echo $2
# cli param1 param2
```

### Check param is (not) empty

```bash
if [ -z "$1" ]; then
    echo "empty param"
fi

if [ ! -z "$1" ]; then
    echo "not empty param"
fi
```

### Bash Equals-Separated (e.g., --option=argument) (without getopt[s]) [^opt]

[^opt]: [How do I parse command line arguments in Bash?](https://stackoverflow.com/questions/192249/how-do-i-parse-command-line-arguments-in-bash)

```bash
#!/bin/bash

for i in "$@"
do
case $i in
    -e=*|--extension=*)
    EXTENSION="${i#*=}"
    shift # past argument=value
    ;;
    -s=*|--searchpath=*)
    SEARCHPATH="${i#*=}"
    shift # past argument=value
    ;;
    -l=*|--lib=*)
    LIBPATH="${i#*=}"
    shift # past argument=value
    ;;
    --default)
    DEFAULT=YES
    shift # past argument with no value
    ;;
    *)
          # unknown option
    ;;
esac
done
echo "FILE EXTENSION  = ${EXTENSION}"
echo "SEARCH PATH     = ${SEARCHPATH}"
echo "LIBRARY PATH    = ${LIBPATH}"
echo "DEFAULT         = ${DEFAULT}"
```


## Varable

### Put value to dynamiclly varable 

```
A_VAR='a'
eval "$1_VAR"='cc'
echo $A_VAR
```

### reference a file for variables [^stackoverflow_bash]

[^stackoverflow_bash]: [How to reference a file for variables using Bash?](https://stackoverflow.com/questions/5228345/how-to-reference-a-file-for-variables-using-bash) and [How to include file in a bash shell script](https://stackoverflow.com/questions/10823635/how-to-include-file-in-a-bash-shell-script)

```bash
source FILE
# or
. FILE

```

## Path

### Source path

#### Dirname
```bash
$(dirname "$0")
```

#### Source path
```bash
SOURCE="${BASH_SOURCE[0]}"
echo $SOURCE
```

#### Source directory path [^source_directory]

[^source_directory]: [Get the source directory of a Bash script from within the script itself](https://stackoverflow.com/questions/59895/get-the-source-directory-of-a-bash-script-from-within-the-script-itself)

```bash
DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd )"
```

### Execution directory

```bash
echo $(pwd)
```


## File and directory
Getting the contents of a directory using shell script. [^1]

[^1]: [How to get the list of files in a directory in a shell script?](https://stackoverflow.com/questions/2437452/how-to-get-the-list-of-files-in-a-directory-in-a-shell-script)

```bash
for entry in "$search_dir"/*
do
  echo "$entry"
done

```

### Check directory
```bash
if [ -d "$DIR" ]; then
    exit 0
else
	exit 1
fi
```

## Conditionals [^taniarascia]

[^taniarascia]: [How to Create and Use Bash Scripts](https://www.taniarascia.com/how-to-create-and-use-bash-scripts/)

Bash Operator | Operator | Description
------------ | ------------- | ------------
`-eq` | `==`  | Equal
`-ne` | `!=`  | Not equal
`-gt` | `>` | Greater than
`-ge` | `>=` |  Greater than or equal
`-lt` | `<`  |  Less than
`-le` | `<=`  | Less than or equal
`-z` | `==`  | null Is null

## Looping [^looping]

[^looping]: [Looping in bash](https://www.taniarascia.com/how-to-create-and-use-bash-scripts/#looping)

```bash
#!/bin/bash

FILES=/Users/tania/dev/*

for file in $FILES
do
    echo $(basename $file)
done

```

## Color 

You can use these ANSI escape codes:[^color]

[^color]: [How to change the output color of echo in Linux](https://stackoverflow.com/questions/5947742/how-to-change-the-output-color-of-echo-in-linux)

```bash
#    .---------- constant part!
#    vvvv vvvv-- the code from above
RED='\033[0;31m'
NC='\033[0m' # No Color
printf "I ${RED}love${NC} Stack Overflow\n"
```

```bash
#!/bin/bash

RED='\033[0;31m'
YELLO='\033[1;33m'
GREEN='\033[0;32m'
NC='\033[0m' # No Color
echo -e "I ${RED}love${NC} coding"
echo -e "I ${YELLO}love${NC} coding"
echo -e "I ${GREEN}love${NC} coding"
```

Color | Code | Color | Code
------------ | ------------- | ------------ | -------------
Black         | `0;30m`   |   Dark Gray     | `1;30m`
Red           | `0;31m`   |   Light Red     | `1;31m`
Green         | `0;32m`   |   Light Green   | `1;32m`
Brown/Orange  | `0;33m`   |   Yellow        | `1;33m`
Blue          | `0;34m`   |   Light Blue    | `1;34m`
Purple        | `0;35m`   |   Light Purple  | `1;35m`
Cyan          | `0;36m`   |   Light Cyan    | `1;36m`
Light Gray    | `0;37m`   |   White         | `1;37m`


## functions
```bash
function get_string()
{
	echo "string"
}

STRING=$(get_string)

```

### Pass params into function [^fun_params]

[^fun_params]: [Bash Scripting Tutorial - 7. Functions!](https://ryanstutorials.net/bash-scripting-tutorial/bash-functions.php)

```bash
function get_string()
{
        echo "$1"
}


STRING=$(get_string aaa)

echo $STRING
```

---

