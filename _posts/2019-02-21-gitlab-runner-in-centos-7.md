---
layout: post
title: Gitlab runner in centos 7
date: 2019-02-21 02:46 +0000
---

## Install into CentOS 7 [^4]

[^4]: [Install GitLab Runner manually on GNU/Linux](https://docs.gitlab.com/runner/install/linux-manually.html)

### Prepare

```bash
yum update -y
yum install wget git openssl ca-certificates -y

```

### Install 

#### Standalone binaries [^5]

[^5]: [GitLab Runner bleeding edge releases](https://docs.gitlab.com/runner/install/bleeding-edge.html)

```bash
wget -O /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64
# or
wget -O /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-386

chmod +x /usr/local/bin/gitlab-runner

useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash

gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner


```

#### Package 

##### Ubuntu

##### CentOS

```
wget https://s3.amazonaws.com/gitlab-runner-downloads/master/rpm/gitlab-runner_amd64.rpm
# or
wget https://s3.amazonaws.com/gitlab-runner-downloads/master/rpm/gitlab-runner_i686.rpm

rpm -i gitlab-runner_amd64.rpm
# or
rpm -i gitlab-runner_i686.rpm

```


```bash
docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock centos /bin/bash

```

* [Official gitlab runner dockerfile](https://hub.docker.com/r/gitlab/gitlab-runner/dockerfile)
* [Install GitLab Runner manually on GNU/Linux](https://docs.gitlab.com/runner/install/linux-manually.html)


## Register Gitlab runner [^1]

[^1]: [Registering Runners](https://docs.gitlab.com/runner/register/index.html)

```
gitlab-runner register
```

## Gitlab runner link to docker in docker

Run gitlab runner docker, and also can building, and run docker image in runner. [^3]

[^3]: [Run GitLab Runner in a container](https://docs.gitlab.com/runner/install/docker.html)

```
 docker run -it --name gitlab-runner --restart always \
   -v /Users/Shared/gitlab-runner/config:/etc/gitlab-runner \
   -v /var/run/docker.sock:/var/run/docker.sock \
   gitlab/gitlab-runner:latest


docker run -it --rm -v /Users/Shared/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner

install


```

Docker runner may also need register [^2]

[^2]: [One-line registration command](https://docs.gitlab.com/runner/register/index.html#docker)

```
docker run -it --rm -v /Users/Shared/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner register
# or 
docker run -it --rm -v /Users/Shared/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner


```


**config.toml**

```json
concurrent = 1
check_interval = 0

[session_server]
  session_timeout = 1800

[[runners]]
  name = "test"
  url = "https://gitlab.com.au/"
  token = "token-string"
  executor = "docker"
  [runners.docker]
    tls_verify = false
    image = "php"
    privileged = false
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/cache"]
    shm_size = 0
  [runners.cache]
    [runners.cache.s3]
    [runners.cache.gcs]

```







---

