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