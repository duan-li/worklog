---
layout: page
title: Docker
---

##  Basic usage
**Get Image**
```
docker pull <image name>
```

**Run Image as container**
```
docker run -it --name="container-name" -v ~/Code:/Code <image name:imageversion> /bin/bash
```

**Rerun same container**
```
docker start -ai container-name
```

**Stop container**
```
docker rm container-name
```

## Push local image to Hub
**Set environment variable**
```
export DOCKER_ID_USER="username"
```

**Login**
```
docker login
```

**Tag your image**
```
docker tag local_image_name $DOCKER_ID_USER/hub_image_repo:tag_name
```

**Push image**
```
docker push $DOCKER_ID_USER/hub_image_repo:tag_name
```

**Save image as `tar` file** [^1]
```
docker save -o path_to/filename.tar image_name:tag_name
```
[^1]: [How to copy Docker images from one host to another without using a repository](https://stackoverflow.com/questions/23935141/how-to-copy-docker-images-from-one-host-to-another-without-using-a-repository)

**Load image from `tar` file**
```
docker load -i path_to/filename.tar
```

**Build image from scratch** [^2]


```bash
# Create a folder for our new root structure
$ export centos_root='/centos_image/rootfs'
$ mkdir -p $centos_root
# initialize rpm database
$ rpm --root $centos_root --initdb
# download and install the centos-release package, it contains our repository sources
$ yum reinstall --downloadonly --downloaddir . centos-release
$ rpm --nodeps --root $centos_root -ivh centos-release*.rpm
$ rpm --root $centos_root --import  $centos_root/etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
# install yum without docs and install only the english language files during the process
$ yum -y --installroot=$centos_root --setopt=tsflags='nodocs' --setopt=override_install_langs=en_US.utf8 install yum
# configure yum to avoid installing of docs and other language files than english generally
$ sed -i "/distroverpkg=centos-release/a override_install_langs=en_US.utf8\ntsflags=nodocs" $centos_root/etc/yum.conf
# chroot to the environment and install some additional tools
$ cp /etc/resolv.conf $centos_root/etc
$ chroot $centos_root /bin/bash <<EOF
yum install -y procps-ng iputils
yum clean all
EOF
$ rm -f $centos_root/etc/resolv.conf

```

```bash
tar -C $centos_root -c . | docker import - centos
```

[^2]: [Creating minimal CentOS docker image from scratch](https://gist.github.com/silveraid/e6bdf78441c731a30a66fc6adca6f4b5)

## Docker image
### Based image
- [How do I create a CentOS Docker image?](https://www.quora.com/How-do-I-create-a-CentOS-Docker-image)
- [Create a base image](https://docs.docker.com/develop/develop-images/baseimages/)
- [Creating Docker BaseImage from ISO](https://github.com/EricWang8230/Note/blob/master/docker/Creating-Docker-BaseImage-from-CentOS-ISO.md)
- [Example CentOS based image](https://github.com/CentOS/sig-cloud-instance-images/tree/CentOS-7.2.1511/docker)

## Docker security
- [5 Best Practices to Container Image Security](https://www.twistlock.com/2017/08/31/container-image-security-best-practices/)
- [Five Docker Security Best Practices](https://thenewstack.io/5-docker-security-best-practices/)
- [Docker Security Best Practices: Part 3 – Securing Container Images](https://anchore.com/blog/docker-security-best-practices-part-3-securing-container-images/)
- [10 layers of Linux container security](https://opensource.com/article/17/10/10-layers-container-security)
- [Docker Image 在 DevOps 流程中的应用](https://www.ibm.com/developerworks/cn/devops/1601_kongyi_devopsdockerimages/index.html)
- [浅谈Docker安全性支持](http://dockone.io/article/8266)
- [从自身漏洞与架构缺陷，谈Docker安全建设](http://www.yunweipai.com/archives/21610.html)
- [如何加固你的微服务容器——Part 1](http://dockone.io/article/2620)







## Docker Compose
`docker-compose up`


## Dockerfile

### `CMD` vs `ENTRYPOINT`
>The main purpose of a CMD is to provide defaults for an executing container. These defaults can include an executable, or they can omit the executable, in which case you must specify an ENTRYPOINT instruction as well.

* `CMD` providers default execute file after container started.




# Docker kernel with Go

 - [Namespace]({% post_url 2018-05-21-linux-namespace %})
 - [Control Group]({% post_url 2018-05-21-linux-control-groups %})
 - [AUFS]({% post_url 2018-06-10-union-file-system %})

 # Docker tools
 - [dive](https://github.com/wagoodman/dive) : A tool for exploring a docker image, layer contents, and discovering ways to shrink your Docker image size.

 

 ---

- [GitLab Container Registry](https://docs.gitlab.com/ee/user/project/container_registry.html)
- [GitLab Container Registry administration](https://docs.gitlab.com/ee/administration/container_registry.html)
- [Container Registries You Might Have Missed](https://rancher.com/container-registries-might-missed/)
 
