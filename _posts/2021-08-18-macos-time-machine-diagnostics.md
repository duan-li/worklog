---
layout: post
title: MacOS time machine diagnostics
date: 2021-08-18 03:12 +0000
---

## Time Machine failing: “an error occurred while copying files” [^1]

[^1]: [Link](https://apple.stackexchange.com/questions/267790/time-machine-failing-an-error-occurred-while-copying-files)


```bash
log show --predicate 'subsystem == "com.apple.TimeMachine"' --info --last 4h|grep -i error

# or
log stream --level debug --predicate 'subsystem == "com.apple.TimeMachine"'
```

