---
layout: post
title: Docker in centos 7
date: 2019-02-21 09:51 +0000
---

Docker needs at least CentOS 7 (CentOS Linux release 7.5.1804 (Core)) [^1] 

[^1]: [Get Docker CE for CentOS](https://docs.docker.com/install/linux/docker-ce/centos/#prerequisites)

## Uninstall old versions

```bash
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

## Prepare

### Set up repo

```bash
yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```


**Enable the nightly or test repositories**

```
yum-config-manager --enable docker-ce-nightly
yum-config-manager --disable docker-ce-nightly

yum-config-manager --enable docker-ce-test
```


### Install Docker CE

```
yum install docker-ce docker-ce-cli containerd.io
```

### Start Docker CE

```
systemctl start docker
```

### Check docker detail
```
$ docker version
Client:
 Version:           18.09.2
 API version:       1.39
 Go version:        go1.10.6
 Git commit:        6247962
 Built:             Sun Feb 10 04:13:27 2019
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          18.09.2
  API version:      1.39 (minimum version 1.12)
  Go version:       go1.10.6
  Git commit:       6247962
  Built:            Sun Feb 10 03:47:25 2019
  OS/Arch:          linux/amd64
  Experimental:     false
```

### Grant permisstion to non-root user

```
usermod -a -G docker user-name
```

### Install `docker-compose`

```
yum install docker-compose -y
```



---



