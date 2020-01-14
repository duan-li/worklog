---
layout: post
title: Quick setup Pi
date: 2020-01-14 03:47 +0000
---

## Initial

```bash
$ sudo apt update
$ sudo apt upgrade
$ sudo apt dist-upgrade
$ sudo rpi-update
```

## Config

```bash
$ sudo raspi-config
```

Enable 
 - 5 Interfacing Options > SSHd
 - 5 Interfacing Options > VNC
 - 2 Network options > B2 Wait for network at Boot

## Install


```bash
$ sudo apt docker.io docker-compose nfs-common portmap
```


## NFS
```bash
$ sudo mount -t nfs <ip>:/<dir> /mnt
```

In `/etc/fstab`, add 

```
<ip>:/<dir>		/home/user		nfs 	defaults	0	0
```


## Clean up

```bash
$ sudo apt purge vlc
$ sudo apt autoremove
$ sudo apt autoclean
$ sudo apt clean
```


## Battery

8:08am until 21:28, Unknown capbility, likely 6000mAh.

