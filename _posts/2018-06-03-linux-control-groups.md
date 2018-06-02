---
layout: post
title: Linux Control Groups
date: 2018-06-03 8:58 +0000
---


# Three components
* Cgroup
* Linux subsystem
* Hierarchy

## How they work
* All system `processes` will be added into a root node when created new `hierarchy`.
* one `subsystem` can have only one `hierarchy`
* one `hierarchy` can have many `subsystem`
* one `process` can be member of multiple `cgroups`. but each of `cgroup` must be in different `hierarchy`
* A `sub-process` that fork from `parent-process` can be in same `cgroup` of `parent-process`, also can be moved to other `cgorup`.


## cgroup

```
mkdir cgroup-test
sudo mount -t cgroup -o none,name=cgroup-test cgroup-test ./cgroup-test
```

* cgroup.clone_children
* cgroup.procs
* cgroup.sane_behavior
* notify_on_release
* release_agent
* tasks


## Linux subsystem
* blkio: control accessing (input/ouptpu) of device 
* cpu
* cpuacct
* cpuset: multiple cpu or multiple core cpu
* devices
* freezer: suspend and resume process of cgroup
* memory
* net_cls: classification of network package
* net_prio: priority
* ns: create new cgroup when fork new process in new Namespace.


### cgroup-bin
```
apt-get install cgroup-bin

``` 

**lssubsys**
List all subsystems support by Kernel.


## Hierarchy
link cgroup like tree structure.



