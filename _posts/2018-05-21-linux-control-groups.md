---
layout: post
title: Linux Control Groups
date: 2018-05-21 21:16 +0000
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

**create mount point for hierarchy**
```
$ mkdir cgroup-test
```

**Mount hierarchy**
```
$ sudo mount -t cgroup -o none,name=cgroup-test cgroup-test ./cgroup-test
```

**Below files will be found on cgroup-test**
* cgroup.clone_children: subsystem cpuset will read this file, if value is 1 (default is 0), sub cgroup will apply parent cgroup's cpuset config.
* cgroup.procs: It is group proccess ID of current node in tree.
* cgroup.sane_behavior
* notify_on_release: with release_agent, make sure the last process execute release_agent when exist.
* release_agent: with notify_on_release, A path, clean up cgroup after the last process exist.
* tasks: mark current cgroup's process IDs, add process into this cgroup when write ID into this file.

**Extend two cgroups**
```
/cgroup-test $ sudo mkdir cgroup-1
/cgroup-test $ sudo mkdir cgroup-2
```

**Check tree structure**

```
/cgroup-test $ tree
```

```
.
├── cgroup-1
│   ├── cgroup.clone_children
│   ├── cgroup.procs
│   ├── notify_on_release
│   └── tasks
├── cgroup-2
│   ├── cgroup.clone_children
│   ├── cgroup.procs
│   ├── notify_on_release
│   └── tasks
├── cgroup.clone_children
├── cgroup.procs
├── cgroup.sane_behavior
├── notify_on_release
├── release_agent
└── tasks

```

**Add or move process in cgroup**
A process in hierarchy of Cgrups can only exist in one cgroup node. All processes are defaultly exist on root node, but can be moved to other cgroup node. The only thing to move is write `pid` to tasks of cgroup node.


```
/cgroup-test $ echo $$
8099

/cgroup-test $ cat tasks
...
8099
...

/cgroup-test$ cd cgroup-1
/cgroup-test/cgroup-1$ cat tasks
/cgroup-test/cgroup-1$ sudo sh -c "echo $$ >> tasks"
/cgroup-test/cgroup-1$ cat tasks
8099
17858
/cgroup-test/cgroup-1$ cat /proc/8099/cgroup
12:name=cgroup-test:/cgroup-1
11:freezer:/
10:hugetlb:/
9:pids:/user.slice/user-1000.slice
8:cpu,cpuacct:/user.slice
7:blkio:/user.slice
6:cpuset:/
5:net_cls,net_prio:/
4:memory:/user.slice
3:perf_event:/
2:devices:/user.slice
1:name=systemd:/user.slice/user-1000.slice/session-2.scope
```

**Limit cgroup resource**
When `mount hierarchy`, there is no link between `hierarchy` and subsystem, so can't limit resources by using `cgroup of hierarchy`. But there is default `hierarchy` for every `subsystem`.

```
$ mount | grep memory
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
```
As you can see, `/sys/fs/cgroup/memory` is mount at memory subsystem's hierarchy.

Now, we can create `cgroup` on this `hierarchy` to limit resources like memory

Before this, install stress by `sudo apt-get install stress`.

```
# try stress process with 20M memory without any limitation
/sys/fs/cgroup/memory$ stress --vm-bytes 20m --vm-keep -m 1

# create a cgroup and limit max size memory 10m
/sys/fs/cgroup/memory$ sudo mkdir test-limit-memory && cd test-limit-memory

/sys/fs/cgroup/memory/test-limit-memory$ sudo sh -c "echo "10m" > memory.limit_in_bytes"

/sys/fs/cgroup/memory/test-limit-memory$ sudo sh -c "echo $$ > tasks"
/sys/fs/cgroup/memory/test-limit-memory$ stress --vm-bytes 200m --vm-keep -m 1
```

**How docker working to limit resource**

Docker create cgroup for every container. And using cgroup to limit resources.

```
$ docker run -itd -m 128m --rm --name="tools" dockercraft/mysql-client
$ cd /sys/fs/cgroup/memory/docker/3a4680003809860500984dfcafa9c690bb944314864e6da28f5a947864da6784/
$ cat memory.limit_in_bytes
134217728
```


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


