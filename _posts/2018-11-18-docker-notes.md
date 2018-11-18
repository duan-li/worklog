---
layout: post
title: Docker notes
date: 2018-11-18 05:02 +0000
---

- What docker is
- What docker does
- Why docker better.


## docker images

```bash

docker ps
docker images

docker ps --format $FORMAT

```

## docker container

### docker ps
#### format

```bash

docker ps --format $FORMAT
```



```bash
$ docker ps --format "table {{.ID}}\t{{.Mounts}}"
CONTAINER ID        MOUNTS
fced780016e2        /Users/duan.li…,/Users/duan.li…

$ docker ps --format "table {{.ID}}\t{{.Mounts}}"
CONTAINER ID        MOUNTS
fced780016e2        /Users/duan.li…,/Users/duan.li…

$ docker ps --format "{{.ID}}"
fced780016e2

docker ps --format "{{.ID}}: {{.Command}}"
fced780016e2: "php -S 0.0.0.0:8000…"

docker ps --format "table {{.ID}}\t{{.Labels}}"
CONTAINER ID        LABELS
fced780016e2        org.label-schema.schema-version== 1.0     org.label-schema.name=CentOS Base Image     org.label-schema.vendor=CentOS     org.label-schema.license=GPLv2     org.label-schema.build-date=20180531

```

Placeholder | Description
----- | -----
.ID | Container ID
.Image | Image ID
.Command | Quoted command
.CreatedAt | Time when the container was created.
.RunningFor | Elapsed time since the container was started.
.Ports | Exposed ports.
.Status | Container status.
.Size | Container disk size.
.Names | Container names.
.Labels | All labels assigned to the container.
.Label | Value of a specific label for this container. For example '{{.Label "com.docker.swarm.cpu"}}'
.Mounts | Names of the volumes mounted in this container.
.Networks | Names of the networks attached to this container.


### docker run

* -it
* -d
* --rm
* --memory
* --cpu-shares
* --cpu-quota


### docker exec

#### exec vs run vs start
* start: start one or more stopped containers
* exec: run a command in a running container
* run create a container from image


### docker logs





---