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

**Save image as `tar` file**
```
docker save -o path_to/filename.tar image_name:tag_name
```

**Load image from `tar` file**
```
docker load -i path_to/filename.tar
```


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
