---
layout: post
title: Install Graylog Collector Sidecar on Alpine linux
date: 2019-10-29 21:51 +0000
---

Basicly, download binary package from [repo](https://github.com/Graylog2/collector-sidecar/releases).


```bash
wget https://github.com/Graylog2/collector-sidecar/releases/download/1.0.2/graylog-sidecar-1.0.2.tar.gz
# all file
tar xzf graylog-sidecar-1.0.2.tar.gz
# single file
tar -xzvf graylog-sidecar-1.0.2.tar.gz ./graylog-sidecar/1.0.2/linux/386/graylog-sidecar
mv /graylog-sidecar/1.0.2/linux/386/graylog-sidecar /bin/graylog-sidecar
rm -Rf /graylog-sidecar
rm graylog-sidecar-1.0.2.tar.gz
```

