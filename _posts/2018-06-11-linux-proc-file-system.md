---
layout: post
title: Linux proc file system
date: 2018-06-11 16:31 +0000
---

Directory and file | Comment
------------ | -------------
/proc/N | process PID is N
/proc/N/cmdline | command start process
/proc/N/cwd | link to process current word directory
/proc/N/environ | Env var list for process
/proc/N/exe | link to process executable command file
/proc/N/fd | includes all file desc of process related file
/proc/N/maps | process related memory info
/proc/N/mem | memory space of current process, not readable
/proc/N/root | root directory of process
/proc/N/stat | status of process
/proc/N/statm | memory status of process
/proc/N/status | process status, better than `stat` and `statm`
/proc/self/ | current process


