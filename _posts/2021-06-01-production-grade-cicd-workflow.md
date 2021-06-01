---
layout: post
title: Production grade CICD workflow
date: 2021-06-01 06:42 +0000
---


```mermaid
graph TB
B((Source code storage)) -- pull/checkout/clone --> C(Pipeline)
C(Pipeline) -- Test & build --> D[Application]
D[Application] -- store --> E((Distribution))
A((Infrastructure)) -- provisioning --> G(Instance)
E((Distribution)) -- load --> F(Deployment)
F(Deployment) -- deploy --> G(Instance)
```

### Source code storage providers
* github
* gitlab
* bitbucket


### Pipeline Providers
* github action
* gitlab runner
* bitbucket pipeline
* Jenkins
* circleci
* AWS codebuild


### Distribution Storage providers


As container image
* github package
* docker hub
* gitlab registry
* AWS registry


As Package
* maven


### Infrastructure provider
* AWS
* google cloud
* Azure



### Provisioning tools
* CloudFormation
* Terraform
* Ansible



### Deployment tools
* kubernetes
* docker swarm
* fargate
* mesos
