---
layout: post
title: Linux Namespace
date: 2018-05-21 21:14 +0000
---

* UTS Namespace
   * seprate nodename and domainname, every namespace has own hostname
   * `CLONE_NEWUTS` create new UTS namespace
* IPC Namespace
   * seprate System V IPC and POSIX message queues, every IPC namespace has own System V IPC and POSIX message queues
   * `CLONE_NEWIPC` create new IPC Namespace 
* PID Namespace
   * `CLONE_NEWPID` create new PID namespace
* Mount Namespace
   * `CLONE_NEWNS`  
* User Namespace
* Network Namespace


