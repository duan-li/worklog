---
layout: post
title: The best practices for Kubernetes
date: 2019-01-23 10:00 +0000
---


9 Principles for k8s security [^1]
1. always upgrade to new version for k8s
2. Using RBAC 
3. Using namespace `kubectl get ns`
4. isolate sensitive work load
5. keep meta data safty on cloud
6. create and identify cluster network security strategy `gcloud container clusters list`
7. pod security strategy
8. node security strategy
9. log

[^1]: [9 Principles for k8s security](https://www.kubernetes.org.cn/5016.html)

Also can using `Calico` [^2]

[^2]: [calico on kubernetes](https://www.kubernetes.org.cn/4960.html)


---
