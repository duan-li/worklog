---
layout: post
title: Self hosted online IDE
date: 2020-10-11 05:37 +0000
---

[Code server](https://github.com/cdr/code-server), also [coder.com/](https://coder.com/). [^suggestions]

[^suggestions]: [Self hosted cloud IDE suggestions](https://www.reddit.com/r/selfhosted/comments/ejzjjw/self_hosted_cloud_ide_suggestions/)

For a good experience, we recommend at least: [^request]

[^request]: [requirements](https://github.com/cdr/code-server/blob/v3.5.0/doc/guide.md#requirements)

1 GB of RAM
2 cores

### Run on docker

```bash
# This will start a code-server container and expose it at http://127.0.0.1:8080.
# It will also mount your current directory into the container as `/home/coder/project`
# and forward your UID/GID so that all file system operations occur as your user outside
# the container.
#
# Your $HOME/.config is mounted at $HOME/.config within the container to ensure you can
# easily access/modify your code-server config in $HOME/.config/code-server/config.json
# outside the container.
mkdir -p ~/.config
docker run -it -p 127.0.0.1:8080:8080 \
  -v "$HOME/.config:/home/coder/.config" \
  -v "$PWD:/home/coder/project" \
  -u "$(id -u):$(id -g)" \
  codercom/code-server:latest
```

* [some other awesome project](https://github.com/awesome-selfhosted/awesome-selfhosted#idetools)