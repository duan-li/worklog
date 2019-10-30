---
layout: page
title: Docker
---

##  Basic usage
**Get Image**
```
docker pull <image name>
```

**Build Image**
```
docker build --rm --force-rm --no-cache . -t image-name
```

* `--rm`: Remove intermediate containers after a successful build (default true)
* `--force-rm`: Always remove intermediate containers
* `--no-cache`: Do not use cache when building the image
* `--pull`: Always attempt to pull a newer version of the image

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

**Remove image with all tags** [^a]
`docker images | grep <image-name> | tr -s ' ' | cut -d ' ' -f 2 | xargs -I {} docker rmi <repo-name>/<image-name>:{}`
	
[^a]: [Delete docker image with all tags](https://medium.com/@itseranga/delete-docker-image-with-all-tags-c631f6049530)


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
# -C dir
# -c create
tar -C $centos_root -c . | docker import - centos
```

[^2]: [Creating minimal CentOS docker image from scratch](https://gist.github.com/silveraid/e6bdf78441c731a30a66fc6adca6f4b5)

## Docker image

**Image to `.tar`**

`docker save -o file.tar imagename`

**`tar` to Image**

`docker load -i file.tar`

### Based image
- [How do I create a CentOS Docker image?](https://www.quora.com/How-do-I-create-a-CentOS-Docker-image)
- [Create a base image](https://docs.docker.com/develop/develop-images/baseimages/)
- [Creating Docker BaseImage from ISO](https://github.com/EricWang8230/Note/blob/master/docker/Creating-Docker-BaseImage-from-CentOS-ISO.md)
- [Example CentOS based image](https://github.com/CentOS/sig-cloud-instance-images/tree/CentOS-7.2.1511/docker)
- [Build a CentOS 7 docker image.](https://gist.github.com/keithchambers/dcd137ef6b8a610923ff)
- [Alpine linux docker image docs](https://docs.docker.com/samples/library/alpine/)
- [Apline docker image git repo](https://github.com/gliderlabs/docker-alpine/)
- [Apline release archive files](http://dl-cdn.alpinelinux.org/alpine/v3.8/releases/x86_64/)

### Clean up after building docker image

#### Alpine linux

```bash
apk del <package-name>
rm -rf /var/cache/apk/*
```

#### Centos

```bash
yum clean all
rm -rf /var/cache/yum
```

#### Other 

```bash
pecl clear-cache 
rm -Rf /tmp/pear
```

### Tools minimize size

You can also try to reduce the size of your images using 2 tools [^tools]

[^tools]: [How to reduce the size of RHEL/Centos/Fedora Docker image](https://stackoverflow.com/questions/46089219/how-to-reduce-the-size-of-rhel-centos-fedora-docker-image)

https://github.com/mvanholsteijn/strip-docker-image

and

https://github.com/docker-slim/docker-slim


## Docker security
- [5 Best Practices to Container Image Security](https://www.twistlock.com/2017/08/31/container-image-security-best-practices/)
- [Five Docker Security Best Practices](https://thenewstack.io/5-docker-security-best-practices/)
- [Docker Security Best Practices: Part 3 – Securing Container Images](https://anchore.com/blog/docker-security-best-practices-part-3-securing-container-images/)
- [10 layers of Linux container security](https://opensource.com/article/17/10/10-layers-container-security)
- [Docker Image 在 DevOps 流程中的应用](https://www.ibm.com/developerworks/cn/devops/1601_kongyi_devopsdockerimages/index.html)
- [浅谈Docker安全性支持](http://dockone.io/article/8266)
- [从自身漏洞与架构缺陷，谈Docker安全建设](http://www.yunweipai.com/archives/21610.html)
- [如何加固你的微服务容器——Part 1](http://dockone.io/article/2620)
- [Best practices writing a Dockerfile](https://engineering.bitnami.com/articles/best-practices-writing-a-dockerfile.html)
- [Improve your Dockerfile, best practices](https://dev.to/azure/improve-your-dockerfile-best-practices-5ll)
- [Testing Strategies for Docker Driven Development](https://codefresh.io/docker-tutorial/testing-strategies-for-docker/) [^tools]
- [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [10 Docker Image Security Best Practices](https://snyk.io/blog/10-docker-image-security-best-practices/)
- [Best Practices for working with Dockerfiles](https://medium.com/@nagarwal/best-practices-for-working-with-dockerfiles-fb2d22b78186)

[^tools]: [habitus](http://www.habitus.io/) and [codefresh.io](https://codefresh.io/)

## Docker Compose

* `-f`, `--file FILE`: Specify an alternate compose file (default: docker-compose.yml)

### `up`

`docker-compose up -f docker-compose.yml -d --force-recreate -V`

* `-f`: `docker-compose.yml` file.
* `-d`: Detached mode: Run containers in the background, print new container names. Incompatible with `--abort-on-container-exit`.
* `-V`: `--renew-anon-volumes`, Recreate anonymous volumes instead of retrieving data from the previous containers.
* `--force-recreate`: Recreate containers even if their configuration and image haven't changed.

### `down`

`docker-compose down -v`

* `-v`, `--volumes`: Remove named volumes declared in the `volumes` section of the Compose file and anonymous volumes attached to containers.
* `--remove-orphans`: Remove containers for services not defined in the Compose file


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


 # Docker Label Schema

> Labels allow us to specify the metadata, but all it does is that. The next obvious step is to come up with some kind of a standard set of Labels that third party tools can look for in the Images. [^docker_label_schema]

[^docker_label_schema]: [Let’s make your Docker Image better than 90% of existing ones](https://medium.com/@chamilad/lets-make-your-docker-image-better-than-90-of-existing-ones-8b1e5de950d)

 Build-time labels [^3]

 [^3]: [Label schema rc1](http://label-schema.org/rc1/)

 These are immutable, and can only have one sensible meaning that is defined at build time.

 All labels are OPTIONAL, however if present MUST be prefixed with the namespace `org.label-schema`.

 | Label | Example | Meaning |
 |-------|---------|---------|
 | `build-date` | `org.label-schema.build-date="2016-04-12T23:20:50.52Z"` | This label contains the Date/Time the image was built. The value SHOULD be formatted according to [RFC 3339](https://tools.ietf.org/html/rfc3339). |
 | `name` | `org.label-schema.name = "myname"` | A human friendly name for the image. For example, this could be the name of a microservice in a microservice architecture. |
 | `description` | `org.label-schema.description = "This service does awesome things with other things"` | Text description of the image. May contain up to 300 characters. |
 | `usage` | `org.label-schema.usage= "/usr/doc/app-usage.txt"` | Link to a file in the container or alternatively a URL that provides usage instructions. If a URL is given it SHOULD be specific to this version of the image e.g. `http://docs.example.com/v1.2/usage` rather than `http://docs.example.com/usage` |
 | `url` | `org.label-schema.url="http://postgresql.org"` | URL of website with more information about the product or service provided by the container. |
 | `vcs-url` | `org.label-schema.vcs-url = "https://github.com/nginx/nginx"` | URL for the source code under version control from which this container image was built. |
 | `vcs-ref` | `org.label-schema.vcs-ref = "279FA63"` | Identifier for the version of the source code from which this image was built. For example if the version control system is git this is the SHA. |
 | `vendor` | `org.label-schema.vendor = "Stark Industries"` | The organization that produces this image. |
 | `version` | `org.label-schema.version = "1.2.3"` `org.label-schema.version = "Beta4.2"` `org.label-schema.version = "1.2.2-dirty"` `org.label-schema.version = "my-test"` | Release identifier for the contents of the image. This is entirely up to the user and could be a numeric version number like 1.2.3, or a text label.<br> The version MAY match a label or tag in the source code repository.<br> You should make sure that only images that exactly reflect a version of code should have that version label. If Julia finds a version 0.7.1 in a repository she SHOULD be able to infer this matches version 0.7.1 of the associated code (and in particular, not 0.7.1 plus some later commits).<br> You SHOULD omit the version label, or use a marker like "dirty" or "test" to indicate when a container image does not match a labelled / tagged version of the code. |
 | `schema-version` | `org.label-schema.schema-version = "1.0"` | This label SHOULD be present to indicate the version of Label Schema in use. |
 | `docker.cmd` | `org.label-schema.docker.cmd= "docker run -d -p 5000:5000 -v config.json:/etc/config.json myapp"` | How to run a container based on the image under the Docker runtime. |
 | `docker.cmd.devel` | `org.label-schema.docker.cmd.devel = "docker run -d -p 5050:5050 -e ENV=DEV myapp"` | How to run the container in development mode under the Docker runtime e.g. with debug tooling or more verbose output. |
 | `docker.cmd.test` | `org.label-schema.docker.cmd.test = "docker run myapp runtests"` | How to run the bundled test-suite for the image under the Docker runtime. MUST execute tests then exit, returning output on stdout and exit with a non-zero exit code on failure. |
 | `docker.cmd.debug` | `org.label-schema.docker.debug = "docker exec -it $CONTAINER /bin/redis-cli"` | How to get an appropriate interactive shell for debugging on the container under Docker. |
 | `docker.cmd.help` | `org.label-schema.docker.cmd.help = "docker exec -it $CONTAINER /bin/app --help"` | How to output help from the image under the docker runtime. The container MUST print this information to stdout and then exit. |
 | `docker.params` | `org.label-schema.docker.params = "NO_THREADS=integer number of threads to launch"` | Applicable environment variables for the Docker runtime. Multiple environment variables can be specified by separating with commas. |
 | `rkt.cmd` | `org.label-schema.rkt.cmd= "rkt run --port=5000-tcp:5000 myapp.aci"` | How to run a container based on the image under the rkt runtime. |
 | `rkt.cmd.devel` | `org.label-schema.rkt.cmd.devel = "rkt run --port=5000-tcp:5000 --set-env=ENV=DEV myapp.aci"` | How to run the container in development mode under the rkt runtime e.g. with debug tooling or more verbose output. |
 | `rkt.cmd.test` | `org.label-schema.rkt.cmd.test = "rkt run --port=5000-tcp:5000 myapp.aci -- runtests"` | How to run the bundled test-suite for the image under the rkt runtime. MUST execute tests then exit, returning output on stdout and exit with a non-zero exit code on failure. |
 | `rkt.cmd.debug` | `org.label-schema.rkt.debug = "rkt enter $CONTAINER --app=/bin/redis-cli"` | How to get an appropriate interactive shell for debugging on the container under rkt. |
 | `rkt.cmd.help` | `org.label-schema.rkt.cmd.help = "rkt enter $CONTAINER --app=/bin/help"` | How to output help from the image under the rkt runtime. The container MUST print this information to stdout and then exit. |
 | `rkt.params` | `org.label-schema.rkt.params = "NO_THREADS=integer number of threads to launch"` | Applicable environment variables for the rkt runtime. Multiple environment variables can be specified by separating with commas. |


# Docker Development API

- [Docker SDK for Python](https://docker-py.readthedocs.io/en/stable/)




# Docker Image Registry

- [GitLab Container Registry](https://docs.gitlab.com/ee/user/project/container_registry.html)
- [GitLab Container Registry administration](https://docs.gitlab.com/ee/administration/container_registry.html)
- [Container Registries You Might Have Missed](https://rancher.com/container-registries-might-missed/)


 ---