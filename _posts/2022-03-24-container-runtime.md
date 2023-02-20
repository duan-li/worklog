---
layout: post
title: Container runtime and alternatives
date: 2022-03-24 11:03 +0000
---

A container runtime, also known as a container engine, is a software component responsible for running and managing containers on a host system. It is a crucial part of containerization technologies like Docker and Kubernetes. The container runtime provides the necessary infrastructure and functionality to create, deploy, and manage containers efficiently.

Popular container runtimes include Docker's `containerd`, `runc`, and `CRI-O`. These runtimes interact with the underlying containerization platform or orchestrator, such as Docker Swarm or Kubernetes, to manage containers at scale and provide additional features like load balancing, auto-scaling, and high availability.



## Alternatives of Docker desktop

### Podman

[Podman](https://podman.io/) is an open-source container runtime and toolset that allows users to manage containers and container images. It is an alternative to Docker, offering a compatible interface while operating with a different architecture. Podman is primarily focused on providing a daemonless container runtime, which means it does not require a separate background service or daemon to run containers.


### Lima

[Lima](https://github.com/lima-vm/lima) is an open-source project that provides a simple and lightweight way to create and manage Linux virtual machines (VMs) for development and testing purposes on macOS. It allows developers to run a Linux environment within a VM without the need for complex setup or virtualization tools.




## References

* [Replace Docker Desktop with lima](https://itnext.io/replace-docker-desktop-with-lima-88ec6f9d6a19)
* https://blog.csdn.net/zhonglinzhang/article/details/76573918


