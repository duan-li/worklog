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

## Docker Compose
`docker-compose up`


# Docker kernel with Go

 - [Namespace]({% post_url 2018-05-21-linux-namespace %})
 - [Control Group]({% post_url 2018-06-03-linux-control-groups %})
