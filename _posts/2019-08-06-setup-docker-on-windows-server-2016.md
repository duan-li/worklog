---
layout: post
title: Setup docker on Windows Server 2016
date: 2019-08-06 00:46 +0000
---

## Install Docker Engine - Enterprise

### Fix connection issue [^1]
```shell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
```

[^1]: [Trying to install program using Powershell and getting this error](https://answers.microsoft.com/en-us/windows/forum/windows_7-performance/trying-to-install-program-using-powershell-and/4c3ac2b2-ebd4-4b2a-a673-e283827da143)

### Install Docker EE [^2]
```shell
Install-Module DockerMsftProvider -Force
Install-Package Docker -ProviderName DockerMsftProvider -Force
```

[^2]: [https://docs.docker.com/install/windows/docker-ee/](https://docs.docker.com/install/windows/docker-ee/)


## Old docker version [^3]

[^3]: [Setup Docker on Windows Server 2016](https://blog.couchbase.com/setup-docker-windows-server-2016/)

### Install the container feature:

```shell
Install-WindowsFeature containers
```

### Restart the Virtual Machine:

Using `Operation System: Reconfiguration (Planned)`


### Base operating system can be installed using ContainerImage PowerShell module. Install the module as:

```shell
Install-PackageProvider ContainerImage -Force
```


## Microsoft-Windows-Subsystem-Linux

* Windows 10 x64 build 14316 or later (note - LTSB builds do not currently support WSL)
* Windows Server build 16237 or later [^4]

[^4]: [Feature name Microsoft-Windows-Subsystem-Linux is unknown](https://github.com/MicrosoftDocs/WSL/issues/226)



---