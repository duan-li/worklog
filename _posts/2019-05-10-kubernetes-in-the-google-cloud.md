---
layout: post
title: Kubernetes in the Google Cloud
date: 2019-05-10 03:39 +0000
---

## Kubernetes Engine: Qwik Start
### Setting a default compute zone

```

gcloud config set compute/zone us-central1-a
```

Return 
```
Updated property [compute/zone].
```

### Creating a Kubernetes Engine cluster

```
gcloud container clusters create [CLUSTER-NAME]
```

```
gcloud container clusters create c111
```


### Get authentication credentials for the cluster


```
gcloud container clusters get-credentials [CLUSTER-NAME]

```



```
gcloud container clusters get-credentials c111

```


### Deploying an application to the cluster

```
kubectl run hello-server --image=gcr.io/google-samples/hello-app:1.0 --port 8080
```


output 
```
deployment.apps "hello-server" created
```

This Kubernetes command creates a Deployment object that represents hello-app. In this command:

* --image specifies a container image to deploy. In this case, the command pulls the example image from a Google Container Registry bucket. gcr.io/google-samples/hello-app:1.0 indicates the specific image version to pull. If a version is not specified, the latest version is used.

* --port specifies the port that the container exposes.

Now create a Kubernetes Service, which is a Kubernetes resource that lets you expose your application to external traffic, by running the following kubectl expose command:

```
kubectl expose deployment hello-server --type="LoadBalancer"
```

output

```
service "hello-server" exposed
```


Inspect the hello-server Service by running kubectl get:

```
kubectl get service hello-server
```

### Clean up

```
gcloud container clusters delete [CLUSTER-NAME]
```

```
gcloud container clusters delete c111
```
## Orchestrating the Cloud with Kubernetes



---