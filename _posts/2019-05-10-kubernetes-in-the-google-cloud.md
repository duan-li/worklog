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

Kubernetes is all about applications. In this part of the lab you will use an example application called "app" to complete the labs.

> App is hosted on GitHub and provides an example 12-Factor application. During this lab you will be working with the following Docker images:

* kelseyhightower/monolith - Monolith includes auth and hello services.
* kelseyhightower/auth - Auth microservice. Generates JWT tokens for authenticated users.
* kelseyhightower/hello - Hello microservice. Greets authenticated users.
* ngnix - Frontend to the auth and hello services.


### Google Kubernetes Engine

In the cloud shell environment type the following command to set the zone:

```
gcloud config set compute/zone us-central1-b
```

After you set the zone, start up a cluster for use in this lab:

```
gcloud container clusters create io
```


### Get the sample code
Clone the GitHub repository from the Cloud Shell command line:
```
git clone https://github.com/googlecodelabs/orchestrate-with-kubernetes.git

cd orchestrate-with-kubernetes/kubernetes
```
List the files to see what you're working with:
```
ls
```
The sample has the following layout:
```
deployments/  /* Deployment manifests */
  ...
nginx/        /* nginx config files */
  ...
pods/         /* Pod manifests */
  ...
services/     /* Services manifests */
  ...
tls/          /* TLS certificates */
  ...
cleanup.sh    /* Cleanup script */
```
Now that you have the code -- it's time to give Kubernetes a try!


### Quick Kubernetes Demo
The easiest way to get started with Kubernetes is to use the kubectl run command. Use it to launch a single instance of the nginx container:
```
kubectl run nginx --image=nginx:1.10.0
```
Kubernetes has created a deployment -- more about deployments later, but for now all you need to know is that deployments keep the pods up and running even when the nodes they run on fail.

In Kubernetes, all containers run in a pod. Use the kubectl get pods command to view the running nginx container:
```
kubectl get pods
```
Once the nginx container is running you can expose it outside of Kubernetes using the kubectl expose command:
```
kubectl expose deployment nginx --port 80 --type LoadBalancer
```
So what just happened? Behind the scenes Kubernetes created an external Load Balancer with a public IP address attached to it. Any client who hits that public IP address will be routed to the pods behind the service. In this case that would be the nginx pod.

List our services now using the kubectl get services command:
```
kubectl get services
```
> Note: It may take a few seconds before the ExternalIP field is populated for your service. This is normal -- just re-run the kubectl get services command every few seconds until the field populates.

Add the External IP to this command to hit the Nginx container remotely:
```
curl http://<External IP>:80
```
And there you go! Kubernetes supports an easy to use workflow out of the box using the kubectl run and expose commands.



## Pods
At the core of Kubernetes is the [Pod](http://kubernetes.io/docs/user-guide/pods/).

Pods represent and hold a collection of one or more containers. Generally, if you have multiple containers with a hard dependency on each other, you package the containers inside a single pod.


In this example there is a pod that contains the monolith and nginx containers.

Pods also have [Volumes](http://kubernetes.io/docs/user-guide/volumes/). Volumes are data disks that live as long as the pods live, and can be used by the containers in that pod. Pods provide a shared namespace for their contents which means that the two containers inside of our example pod can communicate with each other, and they also share the attached volumes.

Pods also share a network namespace. This means that there is one IP Address per pod.

Now let's take a deeper dive into pods.



### Creating Pods


Pods can be created using pod configuration files. Let's take a moment to explore the monolith pod configuration file. Run the following:
```
cat pods/monolith.yaml
```
The output shows the open configuration file:
```
apiVersion: v1
kind: Pod
metadata:
  name: monolith
  labels:
    app: monolith
spec:
  containers:
    - name: monolith
      image: kelseyhightower/monolith:1.0.0
      args:
        - "-http=0.0.0.0:80"
        - "-health=0.0.0.0:81"
        - "-secret=secret"
      ports:
        - name: http
          containerPort: 80
        - name: health
          containerPort: 81
      resources:
        limits:
          cpu: 0.2
          memory: "10Mi"

```

There's a few things to notice here. You'll see that:

* your pod is made up of one container (the monolith).
* you're passing a few arguments to our container when it starts up.
* you're opening up port 80 for http traffic.



Create the monolith pod using kubectl:
```
kubectl create -f pods/monolith.yaml
```

Examine your pods. Use the kubectl get pods command to list all pods running in the default namespace:

```
kubectl get pods
```

> Note: It may take a few seconds before the monolith pod is up and running. The monolith container image needs to be pulled from the Docker Hub before we can run it.

```
cat pods/monolith.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: monolith
  labels:
    app: monolith
spec:
  containers:
    - name: monolith
      image: kelseyhightower/monolith:1.0.0
      args:
        - "-http=0.0.0.0:80"
        - "-health=0.0.0.0:81"
        - "-secret=secret"
      ports:
        - name: http
          containerPort: 80
        - name: health
          containerPort: 81
      resources:
        limits:
          cpu: 0.2
          memory: "10Mi"
```




Once the pod is running, use kubectl describe command to get more information about the monolith pod:
```
kubectl describe pods monolith
```
You'll see a lot of the information about the monolith pod including the Pod IP address and the event log. This information will come in handy when troubleshooting.

Kubernetes makes it easy to create pods by describing them in configuration files and easy to view information about them when they are running. At this point you have the ability to create all the pods your deployment requires!


### Interacting with Pods

By default, pods are allocated a private IP address and cannot be reached outside of the cluster. Use the `kubectl port-forward` command to map a local port to a port inside the monolith pod.

> From this point on the lab will ask you to work in multiple cloud shell tabs to set up communication between the pods. Any commands that are executed in a second or third command shell will be denoted in the command's instructions.

Open two Cloud Shell terminals. One to run the `kubectl port-forward` command, and the other to issue `curl` commands.


Open two Cloud Shell terminals. One to run the kubectl port-forward command, and the other to issue curl commands.

In the **2nd terminal**, run this command to set up port-forwarding:

```
kubectl port-forward monolith 10080:80
```
Now in the **1st terminal** start talking to your pod using `curl`:
```
curl http://127.0.0.1:10080
```
Yes! You got a very friendly "hello" back from your container.

Now use the curl command to see what happens when you hit a secure endpoint:
```
curl http://127.0.0.1:10080/secure
```
Uh oh.

Try logging in to get an auth token back from the monolith:
```
curl -u user http://127.0.0.1:10080/login
```
At the login prompt, use the super-secret password "password" to login.

Logging in caused a JWT token to print out. Since cloud shell does not handle copying long strings well, create an environment variable for the token.
```
TOKEN=$(curl http://127.0.0.1:10080/login -u user|jq -r '.token')
```
Enter the super-secret password "password" again when prompted for the host password.

Use this command to copy and then use the token to hit the secure endpoint with curl:


```
curl -H "Authorization: Bearer $TOKEN" http://127.0.0.1:10080/secure

```
At this point you should get a response back from our application, letting us know everything is right in the world again.

Use the kubectl logs command to view the logs for the monolith Pod.
```
kubectl logs monolith
```
Open a **3rd terminal** and use the -f flag to get a stream of the logs happening in real-time:
```
kubectl logs -f monolith
```
Now if you use curl in the **1st terminal** to interact with the monolith, you can see the logs updating (in the **3rd terminal**):
```
curl http://127.0.0.1:10080
```
Use the kubectl exec command to run an interactive shell inside the Monolith Pod. This can come in handy when you want to troubleshoot from within a container:
```
kubectl exec monolith --stdin --tty -c monolith /bin/sh
```
For example, once we have a shell into the monolith container we can test external connectivity using the ping command:
```
ping -c 3 google.com
```
Be sure to log out when you're done with this interactive shell.
```
exit
```
As you can see, interacting with pods is as easy as using the kubectl command. If you need to hit a container remotely, or get a login shell, Kubernetes provides everything you need to get up and going.



### Services

Pods aren't meant to be persistent. They can be stopped or started for many reasons - like failed liveness or readiness checks - and this leads to a problem:

What happens if you want to communicate with a set of Pods? When they get restarted they might have a different IP address.

That's where [Services](http://kubernetes.io/docs/user-guide/services/) come in. Services provide stable endpoints for Pods.


Services use labels to determine what Pods they operate on. If Pods have the correct labels, they are automatically picked up and exposed by our services.

The level of access a service provides to a set of pods depends on the Service's type. Currently there are three types:

* `ClusterIP` (internal) -- the default type means that this Service is only visible inside of the cluster,
* `NodePort` gives each node in the cluster an externally accessible IP and
* `LoadBalancer` adds a load balancer from the cloud provider which forwards traffic from the service to Nodes within it.

Now you'll learn how to:

* Create a service
* Use label selectors to expose a limited set of Pods externally


### Creating a Service


Before we can create our services -- let's first create a secure pod that can handle https traffic.

If you've changed directories, make sure you return to the ~/orchestrate-with-kubernetes/kubernetes directory:
```
cd ~/orchestrate-with-kubernetes/kubernetes
```

Explore the monolith service configuration file:
```
cat pods/secure-monolith.yaml
```
Create the secure-monolith pods and their configuration data:
```
kubectl create secret generic tls-certs --from-file tls/
kubectl create configmap nginx-proxy-conf --from-file nginx/proxy.conf
kubectl create -f pods/secure-monolith.yaml
```
Now that you have a secure pod, it's time to expose the secure-monolith Pod externally.To do that, create a Kubernetes service.

Explore the monolith service configuration file:

cat services/monolith.yaml

(Output):
```
kind: Service
apiVersion: v1
metadata:
  name: "monolith"
spec:
  selector:
    app: "monolith"
    secure: "enabled"
  ports:
    - protocol: "TCP"
      port: 443
      targetPort: 443
      nodePort: 31000
  type: NodePort
```

Things to note:

* There's a selector which is used to automatically find and expose any pods with the labels "app=monolith" and "secure=enabled"
* Now you have to expose the nodeport here because this is how we'll forward external traffic from port 31000 to nginx (on port 443).
* Use the `kubectl create` command to create the monolith service from the monolith service configuration file:

kubectl create -f services/monolith.yaml

(Output):
```
service "monolith" created
```
#### Firewall
You're using a port to expose the service. This means that it's possible to have port collisions if another app tries to bind to port 31000 on one of your servers.

Normally, Kubernetes would handle this port assignment. In this lab you chose a port so that it's easier to configure health checks later on.

Use the gcloud compute firewall-rules command to allow traffic to the monolith service on the exposed nodeport:
```
gcloud compute firewall-rules create allow-monolith-nodeport \
  --allow=tcp:31000
```


Now that everything is setup you should be able to hit the secure-monolith service from outside the cluster without using port forwarding.

First, get an external IP address for one of the nodes.
```
gcloud compute instances list
```
Now try hitting the secure-monolith service using curl:

```
curl -k https://35.224.59.58:31000
curl -k https://<EXTERNAL_IP>:31000

```

It's time for a quick knowledge check.Use the following commands to answer the questions below.

* `kubectl get services monolith`
* `kubectl describe services monolith`

Questions:

* Why are you unable to get a response from the monolith service?
* How many endpoints does the monolith service have?
* What labels must a Pod have to be picked up by the monolith service?


### Adding Labels to Pods

Currently the monolith service does not have endpoints. One way to troubleshoot an issue like this is to use the kubectl get pods command with a label query.

We can see that we have quite a few pods running with the monolith label.
```
kubectl get pods -l "app=monolith"
```
But what about "app=monolith" and "secure=enabled"?
```
kubectl get pods -l "app=monolith,secure=enabled"
```

Notice this label query does not print any results. It seems like we need to add the "secure=enabled" label to them.

Use the kubectl label command to add the missing secure=enabled label to the secure-monolith Pod. Afterwards, you can check and see that your labels have been updated.
```
kubectl label pods secure-monolith 'secure=enabled'
kubectl get pods secure-monolith --show-labels
```

Now that our pods are correctly labeled, let's view the list of endpoints on the monolith service:
```
kubectl describe services monolith | grep Endpoints
```
And you have one!

Let's test this out by hitting one of our nodes again.
```
gcloud compute instances list
curl -k https://<EXTERNAL_IP>:31000
```
Bam! Houston, we have contact.

### Deploying Applications with Kubernetes



The goal of this lab is to get you ready for scaling and managing containers in production. That's where [Deployments](http://kubernetes.io/docs/user-guide/deployments/#what-is-a-deployment) come in. Deployments are a declarative way to ensure that the number of Pods running is equal to the desired number of Pods, specified by the user.


The main benefit of Deployments is in abstracting away the low level details of managing Pods. Behind the scenes Deployments use [Replica Sets](http://kubernetes.io/docs/user-guide/replicasets/) to manage starting and stopping the Pods. If Pods need to be updated or scaled, the Deployment will handle that. Deployment also handles restarting Pods if they happen to go down for some reason.

Let's look at a quick example:


Pods are tied to the lifetime of the Node they are created on. In the example above, Node3 went down (taking a Pod with it). Insteading of manually creating a new Pod and finding a Node for it, your Deployment created a new Pod and started it on Node2.

That's pretty cool!

It's time to combine everything you learned about Pods and Services to break up the monolith application into smaller Services using Deployments.

### Creating Deployments


We're going to break the monolith app into three separate pieces:

* auth - Generates JWT tokens for authenticated users.
* hello - Greet authenticated users.
* frontend - Routes traffic to the auth and hello services.

We are ready to create deployments, one for each service. Afterwards, we'll define internal services for the auth and hello deployments and an external service for the frontend deployment. Once finished you'll be able to interact with the microservices just like with Monolith only now each piece will be able to be scaled and deployed, independently!

Get started by examining the auth deployment configuration file.

```
cat deployments/auth.yaml
```

(Output)
```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: auth
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: auth
        track: stable
    spec:
      containers:
        - name: auth
          image: "kelseyhightower/auth:1.0.0"
          ports:
            - name: http
              containerPort: 80
            - name: health
              containerPort: 81
...
```
The deployment is creating 1 replica, and we're using version 1.0.0 of the auth container.

When you run the kubectl create command to create the auth deployment it will make one pod that conforms to the data in the Deployment manifest. This means you can scale the number of Pods by changing the number specified in the Replicas field.

Anyway, go ahead and create your deployment object:
```
kubectl create -f deployments/auth.yaml
```
It's time to create a service for your auth deployment. Use the kubectl create command to create the auth service:
```
kubectl create -f services/auth.yaml
```
Now do the same thing to create and expose the hello deployment:
```
kubectl create -f deployments/hello.yaml
kubectl create -f services/hello.yaml
```
And one more time to create and expose the frontend Deployment.
```
kubectl create configmap nginx-frontend-conf --from-file=nginx/frontend.conf
kubectl create -f deployments/frontend.yaml
kubectl create -f services/frontend.yaml
```
There is one more step to creating the frontend because you need to store some configuration data with the container.

Interact with the frontend by grabbing it's External IP and then curling to it:
```
kubectl get services frontend
curl -k https://<EXTERNAL-IP>
```
And you get a hello response back!


## Managing Deployments Using Kubernetes Engine

### Set zone

```
gcloud config set compute/zone us-central1-a
```

### Get sample code for this lab
Get the sample code for creating and running containers and deployments:
```
git clone https://github.com/googlecodelabs/orchestrate-with-kubernetes.git
cd orchestrate-with-kubernetes/kubernetes
```
Create a cluster with five n1-standard-1 nodes (this will take a few minutes to complete):
```
gcloud container clusters create bootcamp --num-nodes 5 --scopes "https://www.googleapis.com/auth/projecthosting,storage-rw"
```
### Learn about the deployment object

Let's get started with Deployments. First let's take a look at the Deployment object. The explain command in kubectl can tell us about the Deployment object.
```
kubectl explain deployment
```
We can also see all of the fields using the --recursive option.
```
kubectl explain deployment --recursive
```
You can use the explain command as you go through the lab to help you understand the structure of a Deployment object and understand what the individual fields do.
```
kubectl explain deployment.metadata.name
```

### Create a deployment
Update the deployments/auth.yaml cs file:
```
vi deployments/auth.yaml
```
Start the editor:
```
i
```
Change the image in the containers section of the Deployment to the following:
```
...
containers:
- name: auth
  image: kelseyhightower/auth:1.0.0
...
```
Save the auth.yaml file: press <Esc> then:
```
:wq
```


Now let's create a simple deployment. Examine the deployment configuration file:
```
cat deployments/auth.yaml
```
(Output)
```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: auth
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: auth
        track: stable
    spec:
      containers:
        - name: auth
          image: "kelseyhightower/auth:1.0.0"
          ports:
            - name: http
              containerPort: 80
            - name: health
              containerPort: 81
...
```
Notice how the Deployment is creating one replica and it's using version 1.0.0 of the auth container.

When you run the kubectl create command to create the auth deployment, it will make one pod that conforms to the data in the Deployment manifest. This means we can scale the number of Pods by changing the number specified in the replicas field.

Go ahead and create your deployment object using kubectl create:
```
kubectl create -f deployments/auth.yaml
```
Once you have created the Deployment, you can verify that it was created.
```
kubectl get deployments
```
Once the deployment is created, Kubernetes will create a ReplicaSet for the Deployment. We can verify that a ReplicaSet was created for our Deployment:
```
kubectl get replicasets
```
We should see a ReplicaSet with a name like auth-xxxxxxx

Finally, we can view the Pods that were created as part of our Deployment. The single Pod is created by the Kubernetes when the ReplicaSet is created.
```
kubectl get pods
```
It's time to create a service for our auth deployment. You've already seen service manifest files, so we won't go into the details here. Use the kubectl create command to create the auth service.
```
kubectl create -f services/auth.yaml
```
Now, do the same thing to create and expose the hello Deployment.
```
kubectl create -f deployments/hello.yaml
kubectl create -f services/hello.yaml
```
And one more time to create and expose the frontend Deployment.
```
kubectl create secret generic tls-certs --from-file tls/
kubectl create configmap nginx-frontend-conf --from-file=nginx/frontend.conf
kubectl create -f deployments/frontend.yaml
kubectl create -f services/frontend.yaml
```

> Note: You created a ConfigMap for the frontend.

Interact with the frontend by grabbing its external IP and then curling to it.
```
kubectl get services frontend
curl -ks https://<EXTERNAL-IP>

```

And you get the hello response back.

You can also use the output templating feature of kubectl to use curl as a one-liner:
```
curl -ks https://`kubectl get svc frontend -o=jsonpath="{.status.loadBalancer.ingress[0].ip}"`
```
Test Completed Task
Click Check my progress below to check your lab progress. If you successfully created Kubernetes cluster and Auth, Hello and Frontend deployments, you'll see an assessment score.


### Scale a Deployment

Now that we have a Deployment created, we can scale it. Do this by updating the spec.replicas field. You can look at an explanation of this field using the kubectl explain command again.
```
kubectl explain deployment.spec.replicas
```
The replicas field can be most easily updated using the kubectl scale command:
```
kubectl scale deployment hello --replicas=5
```

> Note: It may take a minute or so for all the new pods to start up.

After the Deployment is updated, Kubernetes will automatically update the associated ReplicaSet and start new Pods to make the total number of Pods equal 5.

Verify that there are now 5 hello Pods running:
```
kubectl get pods | grep hello- | wc -l
```
Now scale back the application:
```
kubectl scale deployment hello --replicas=3
```
Again, verify that you have the correct number of Pods.
```
kubectl get pods | grep hello- | wc -l
```
You learned about Kubernetes deployments and how to manage & scale a group of Pods.



### Rolling update

Deployments support updating images to a new version through a rolling update mechanism. When a Deployment is updated with a new version, it creates a new ReplicaSet and slowly increases the number of replicas in the new ReplicaSet as it decreases the replicas in the old ReplicaSet.

### Trigger a rolling update

To update your Deployment, run the following command:
```
kubectl edit deployment hello
```
Change the image in the containers section of the Deployment to the following:
```
...
containers:
- name: hello
  image: kelseyhightower/hello:2.0.0
...
```
Save and exit.

Once you save out of the editor, the updated Deployment will be saved to your cluster and Kubernetes will begin a rolling update.

See the new ReplicaSet that Kubernetes creates.:
```
kubectl get replicaset
```
You can also see a new entry in the rollout history:
```
kubectl rollout history deployment/hello
```
### Pause a rolling update

If you detect problems with a running rollout, pause it to stop the update. Give that a try now:
```
kubectl rollout pause deployment/hello
```
Verify the current state of the rollout:
```
kubectl rollout status deployment/hello
```
You can also verify this on the Pods directly:
```
kubectl get pods -o jsonpath --template='{range .items[*]}{.metadata.name}{"\t"}{"\t"}{.spec.containers[0].image}{"\n"}{end}'
```

### Resume a rolling update

The rollout is paused which means that some pods are at the new version and some pods are at the older version. We can continue the rollout using the resume command.
```
kubectl rollout resume deployment/hello
```
When the rollout is complete, you should see the following when running the status command.
```
kubectl rollout status deployment/hello
```
(Output)
```
deployment "hello" successfully rolled out

```


### Rollback an update
Assume that a bug was detected in your new version. Since the new version is presumed to have problems, any users connected to the new Pods will experience those issues.

You will want to roll back to the previous version so you can investigate and then release a version that is fixed properly.

Use the rollout command to roll back to the previous version:
```
kubectl rollout undo deployment/hello
```
Verify the roll back in the history:
```
kubectl rollout history deployment/hello
```
Finally, verify that all the Pods have rolled back to their previous versions:
```
kubectl get pods -o jsonpath --template='{range .items[*]}{.metadata.name}{"\t"}{"\t"}{.spec.containers[0].image}{"\n"}{end}'
```
Great! You learned about rolling updates for Kubernetes deployments and how to update applications without downtime.

### Canary deployments

When you want to test a new deployment in production with a subset of your users, use a canary deployment. Canary deployments allow you to release a change to a small subset of your users to mitigate risk associated with new releases.

### Create a canary deployment
A canary deployment consists of a separate deployment with your new version and a service that targets both your normal, stable deployment as well as your canary deployment.


First, create a new canary deployment for the new version:
```
cat deployments/hello-canary.yaml
```
(Output)
```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: hello-canary
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: hello
        track: canary
        # Use ver 1.0.0 so it matches version on service selector
        version: 1.0.0
    spec:
      containers:
        - name: hello
          image: kelseyhightower/hello:2.0.0
          ports:
            - name: http
              containerPort: 80
            - name: health
              containerPort: 81
...
```
Make sure to update version to 1.0.0 (if your version is pointing to any other)

Now create the canary deployment:
```
kubectl create -f deployments/hello-canary.yaml
```
After the canary deployment is created, you should have two deployments, hello and hello-canary. Verify it with this kubectl command:
```
kubectl get deployments
```
On the hello service, the selector uses the app:hello selector which will match pods in both the prod deployment and canary deployment. However, because the canary deployment has a fewer number of pods, it will be visible to fewer users.

### Verify the canary deployment
You can verify the `hello` version being served by the request:
```
curl -ks https://`kubectl get svc frontend -o=jsonpath="{.status.loadBalancer.ingress[0].ip}"`/version
```
Run this several times and you should see that some of the requests are served by hello 1.0.0 and a small subset (1/4 = 25%) are served by 2.0.0.





### Canary deployments in production - session affinity
In this lab, each request sent to the Nginx service had a chance to be served by the canary deployment. But what if you wanted to ensure that a user didn't get served by the Canary deployment? A use case could be that the UI for an application changed, and you don't want to confuse the user. In a case like this, you want the user to "stick" to one deployment or the other.

You can do this by creating a service with session affinity. This way the same user will always be served from the same version. In the example below the service is the same as before, but a new sessionAffinity field has been added, and set to ClientIP. All clients with the same IP address will have their requests sent to the same version of the hello application.
```
kind: Service
apiVersion: v1
metadata:
  name: "hello"
spec:
  sessionAffinity: ClientIP
  selector:
    app: "hello"
  ports:
    - protocol: "TCP"
      port: 80
      targetPort: 80
```
Due to it being difficult to set up an environment to test this, you don't need to here, but you may want to use sessionAffinity for canary deployments in production.


### Blue-green deployments
Rolling updates are ideal because they allow you to deploy an application slowly with minimal overhead, minimal performance impact, and minimal downtime. There are instances where it is beneficial to modify the load balancers to point to that new version only after it has been fully deployed. In this case, blue-green deployments are the way to go.

Kubernetes achieves this by creating two separate deployments; one for the old "blue" version and one for the new "green" version. Use your existing hello deployment for the "blue" version. The deployments will be accessed via a Service which will act as the router. Once the new "green" version is up and running, you'll switch over to using that version by updating the Service.


> A major downside of blue-green deployments is that you will need to have at least 2x the resources in your cluster necessary to host your application. Make sure you have enough resources in your cluster before deploying both versions of the application at once.



### The service
Use the existing hello service, but update it so that it has a selector app:hello, version: 1.0.0. The selector will match the existing "blue" deployment. But it will not match the "green" deployment because it will use a different version.

First update the service:
```
kubectl apply -f services/hello-blue.yaml

```


### Updating using Blue-Green Deployment

In order to support a blue-green deployment style, we will create a new "green" deployment for our new version. The green deployment updates the version label and the image path.
```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: hello-green
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: hello
        track: stable
        version: 2.0.0
    spec:
      containers:
        - name: hello
          image: kelseyhightower/hello:2.0.0
          ports:
            - name: http
              containerPort: 80
            - name: health
              containerPort: 81
          resources:
            limits:
              cpu: 0.2
              memory: 10Mi
          livenessProbe:
            httpGet:
              path: /healthz
              port: 81
              scheme: HTTP
            initialDelaySeconds: 5
            periodSeconds: 15
            timeoutSeconds: 5
          readinessProbe:
            httpGet:
              path: /readiness
              port: 81
              scheme: HTTP
            initialDelaySeconds: 5
            timeoutSeconds: 1
```
Create the green deployment:
```
kubectl create -f deployments/hello-green.yaml
```
Once you have a green deployment and it has started up properly, verify that the current version of 1.0.0 is still being used:
```
curl -ks https://`kubectl get svc frontend -o=jsonpath="{.status.loadBalancer.ingress[0].ip}"`/version
```
Now, update the service to point to the new version:
```
kubectl apply -f services/hello-green.yaml
```
With the service is updated, the "green" deployment will be used immediately. You can now verify that the new version is always being used.
```
curl -ks https://`kubectl get svc frontend -o=jsonpath="{.status.loadBalancer.ingress[0].ip}"`/version
```

### Blue-Green Rollback
If necessary, you can roll back to the old version in the same way. While the "blue" deployment is still running, just update the service back to the old version.
```
kubectl apply -f services/hello-blue.yaml
```
Once you have updated the service, your rollback will have been successful. Again, verify that the right version is now being used:
```
curl -ks https://`kubectl get svc frontend -o=jsonpath="{.status.loadBalancer.ingress[0].ip}"`/version
```
You did it! You learned about blue-green deployments and how to deploy updates to applications that need to switch versions all at once.







## Continuous Delivery with Jenkins in Kubernetes Engine


### Clone Repository
Let's get set up. You'll first set your zone and then clone the lab's sample code into your Cloud Shell:
```
gcloud config set compute/zone us-central1-f

git clone https://github.com/GoogleCloudPlatform/continuous-deployment-on-kubernetes.git

cd continuous-deployment-on-kubernetes
```

### Provisioning Jenkins

#### Creating a Kubernetes cluster
Now, run the following command to provision a Kubernetes cluster:
```
gcloud container clusters create jenkins-cd \
--num-nodes 2 \
--machine-type n1-standard-2 \
--scopes "https://www.googleapis.com/auth/projecthosting,cloud-platform"
```
This step can take up to several minutes to complete. The extra scopes enable Jenkins to access Cloud Source Repositories and Google Container Registry.

Before continuing, confirm that your cluster is running by running the following command:
```
gcloud container clusters list
```
Now, get the credentials for your cluster:
```
gcloud container clusters get-credentials jenkins-cd
```
Kubernetes Engine uses these credentials to access your newly provisioned cluster—confirm that you can connect to it by running the following command:
```
kubectl cluster-info

```



### Install Helm
In this lab, you will use Helm to install Jenkins from the Charts repository. Helm is a package manager that makes it easy to configure and deploy Kubernetes applications. Once you have Jenkins installed, you'll be able to set up your CI/CD pipeline.

1. Download and install the helm binary
```
wget https://storage.googleapis.com/kubernetes-helm/helm-v2.9.1-linux-amd64.tar.gz
```

2. Unzip the file in Cloud Shell:
```
tar zxfv helm-v2.9.1-linux-amd64.tar.gz
cp linux-amd64/helm .
```

3. Add yourself as a cluster administrator in the cluster's RBAC so that you can give Jenkins permissions in the cluster:
```
kubectl create clusterrolebinding cluster-admin-binding --clusterrole=cluster-admin --user=$(gcloud config get-value account)
```

4. Grant Tiller, the server side of Helm, the cluster-admin role in your cluster:
```
kubectl create serviceaccount tiller --namespace kube-system
kubectl create clusterrolebinding tiller-admin-binding --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
```

5. Initialize Helm. This ensures that the server side of Helm (Tiller) is properly installed in your cluster.
```
./helm init --service-account=tiller
./helm update
```

6. Ensure Helm is properly installed by running the following command. You should see versions appear for both the server and the client of v2.9.1:
```
./helm version
```
Example Output:
```
Client: &version.Version{SemVer:"v2.9.1", GitCommit:"20adb27c7c5868466912eebdf6664e7390ebe710", GitTreeState:"clean"}
Server: &version.Version{SemVer:"v2.9.1", GitCommit:"20adb27c7c5868466912eebdf6664e7390ebe710", GitTreeState:"clean"}
```



### Configure and Install Jenkins
You will use a custom values file to add the GCP specific plugin necessary to use service account credentials to reach your Cloud Source Repository.

1. Use the Helm CLI to deploy the chart with your configuration settings.
```
./helm install -n cd stable/jenkins -f jenkins/values.yaml --version 0.16.6 --wait
```

2. Once that command completes ensure the Jenkins pod goes to the Running state and the container is in the READY state:
```
kubectl get pods
```
Example Output:
```
NAME                          READY     STATUS    RESTARTS   AGE
cd-jenkins-7c786475dd-vbhg4   1/1       Running   0          1m
```

3. Run the following command to setup port forwarding to the Jenkins UI from the Cloud Shell
```
export POD_NAME=$(kubectl get pods -l "component=cd-jenkins-master" -o jsonpath="{.items[0].metadata.name}")
kubectl port-forward $POD_NAME 8080:8080 >> /dev/null &
```

4. Now, check that the Jenkins Service was created properly:
```
kubectl get svc
```

Example Output:
```
NAME               CLUSTER-IP     EXTERNAL-IP   PORT(S)     AGE
cd-jenkins         10.35.249.67   <none>        8080/TCP    3h
cd-jenkins-agent   10.35.248.1    <none>        50000/TCP   3h
kubernetes         10.35.240.1    <none>        443/TCP     9h
```

We are using the [Kubernetes Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Kubernetes+Plugin) so that our builder nodes will be automatically launched as necessary when the Jenkins master requests them. Upon completion of their work, they will automatically be turned down and their resources added back to the clusters resource pool.

Notice that this service exposes ports 8080 and 50000 for any pods that match the selector. This will expose the Jenkins web UI and builder/agent registration ports within the Kubernetes cluster. Additionally, the jenkins-ui services is exposed using a ClusterIP so that it is not accessible from outside the cluster.




### Connect to Jenkins
1. The Jenkins chart will automatically create an admin password for you. To retrieve it, run:
```
printf $(kubectl get secret cd-jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo
```
2. To get to the Jenkins user interface, click on the Web Preview button in cloud shell, then click “Preview on port 8080”:

3. You should now be able to log in with username admin and your auto-generated password.

You now have Jenkins set up in your Kubernetes cluster! Jenkins will drive your automated CI/CD pipelines in the next sections.




### Understanding the Application

You'll deploy the sample application, gceme, in your continuous deployment pipeline. The application is written in the Go language and is located in the repo's sample-app directory. When you run the gceme binary on a Compute Engine instance, the app displays the instance's metadata in an info card.

The application mimics a microservice by supporting two operation modes.

* In **backend mode**: gceme listens on port 8080 and returns Compute Engine instance metadata in JSON format.
* In **frontend mode**: gceme queries the backend gceme service and renders the resulting JSON in the user interface.


### Deploying the Application

You will deploy the application into two different environments:

* **Production**: The live site that your users access.
* **Canary**: A smaller-capacity site that receives only a percentage of your user traffic. Use this environment to validate your software with live traffic before it's released to all of your users.


In Google Cloud Shell, navigate to the sample application directory:
```
cd sample-app
```
Create the Kubernetes namespace to logically isolate the deployment:
```
kubectl create ns production
```
Create the production and canary deployments, and the services using the kubectl apply commands:
```
kubectl apply -f k8s/production -n production

kubectl apply -f k8s/canary -n production

kubectl apply -f k8s/services -n production

```

By default, only one replica of the frontend is deployed. Use the kubectl scale command to ensure that there are at least 4 replicas running at all times.

Scale up the production environment frontends by running the following command:
```
kubectl scale deployment gceme-frontend-production -n production --replicas 4
```

Now confirm that you have 5 pods running for the frontend, 4 for production traffic and 1 for canary releases (changes to the canary release will only affect 1 out of 5 (20%) of users):
```
kubectl get pods -n production -l app=gceme -l role=frontend
```

Also confirm that you have 2 pods for the backend, 1 for production and 1 for canary:
```
kubectl get pods -n production -l app=gceme -l role=backend
```
Retrieve the external IP for the production services:
```
kubectl get service gceme-frontend -n production
```

> Note: It can take several minutes before you see the load balancer external IP address.

Example Output:
```
NAME            TYPE          CLUSTER-IP     EXTERNAL-IP     PORT(S)  AGE
gceme-frontend  LoadBalancer  10.79.241.131  104.196.110.46  80/TCP   5h
```

Paste External IP into a browser to see the info card displayed on a card—you should get a similar page:


Now, store the frontend service load balancer IP in an environment variable for use later:
```
export FRONTEND_SERVICE_IP=$(kubectl get -o jsonpath="{.status.loadBalancer.ingress[0].ip}" --namespace=production services gceme-frontend)
```

Confirm that both services are working by opening the frontend external IP address in your browser. Check the version output of the service by running the following command (it should read 1.0.0):
```
curl http://$FRONTEND_SERVICE_IP/version
```

You have successfully deployed the sample application! Next, you will set up a pipeline for deploying your changes continuously and reliably.


### Creating the Jenkins Pipeline

#### Creating a repository to host the sample app source code

Let's create a copy of the gceme sample app and push it to a [Cloud Source Repository](https://cloud.google.com/source-repositories/docs/):
```
gcloud alpha source repos create default
```
You can ignore the warning, you will not be billed for this repository.

```
git init
```
Initialize the sample-app directory as its own Git repository:
```
git config credential.helper gcloud.sh
```
Run the following command:
```
git remote add origin https://source.developers.google.com/p/$DEVSHELL_PROJECT_ID/r/default
```
Set the username and email address for your Git commits. Replace [EMAIL_ADDRESS] with your Git email address and [USERNAME] with your Git username:
```
git config --global user.email "[EMAIL_ADDRESS]"

git config --global user.name "[USERNAME]"
```

Add, commit, and push the files:
```
git add .

git commit -m "Initial commit"

git push origin master
```

#### Adding your service account credentials
Configure your credentials to allow Jenkins to access the code repository. Jenkins will use your cluster's service account credentials in order to download code from the Cloud Source Repositories.

* **Step 1**: In the Jenkins user interface, click Credentials in the left navigation.

* **Step 2**: Click Jenkins 


* **Step 3**: Click Global credentials (unrestricted).

* **Step 4**: Click Add Credentials in the left navigation.

* **Step 5**: Select Google Service Account from metadata from the Kind drop-down and click OK.


The global credentials has been added. The name of the credential is the `GCP Project ID` found in the `CONNECTION DETAILS` section of the lab.


**Creating the Jenkins job**

Navigate to your Jenkins user interface and follow these steps to configure a Pipeline job.

* **Step 1**: **Click Jenkins** > **New Item** in the left navigation:


* **Step 2**: Name the project sample-app, then choose the Multibranch Pipeline option and click OK.

* **Step 3**: On the next page, in the Branch Sources section, click Add Source and select git.

* **Step 4**: Paste the HTTPS clone URL of your sample-app repo in Cloud Source Repositories into the Project Repository field. Replace [PROJECT_ID] with your GCP Project ID:

```
https://source.developers.google.com/p/[PROJECT_ID]/r/default
https://source.developers.google.com/p/qwiklabs-gcp-855b12d51c5deef4/r/default
```


* **Step 5**: From the Credentials drop-down, select the name of the credentials you created when adding your service account in the previous steps.

* **Step 6**: Under Scan Multibranch Pipeline Triggers section, check the Periodically if not otherwise run box and set the Interval value to 1 minute.

* **Step 7**: Your job configuration should look like this:


* **Step 8**: Click Save leaving all other options with their defaults

After you complete these steps, a job named "Branch indexing" runs. This meta-job identifies the branches in your repository and ensures changes haven't occurred in existing branches. If you click sample-app in the top left, the master job should be seen.

> Note: The first run of the master job might fail until you make a few code changes in the next step.

You have successfully created a Jenkins pipeline! Next, you'll create the development environment for continuous integration.



### Creating the Development Environment

Development branches are a set of environments your developers use to test their code changes before submitting them for integration into the live site. These environments are scaled-down versions of your application, but need to be deployed using the same mechanisms as the live environment.

#### Creating a development branch

To create a development environment from a feature branch, you can push the branch to the Git server and let Jenkins deploy your environment.

Create a development branch and push it to the Git server:
```
git checkout -b new-feature
```

#### Modifying the pipeline definition
The Jenkinsfile that defines that pipeline is written using the [Jenkins Pipeline Groovy syntax](https://jenkins.io/doc/book/pipeline/syntax/). Using a `Jenkinsfile` allows an entire build pipeline to be expressed in a single file that lives alongside your source code. Pipelines support powerful features like parallelization and require manual user approval.

In order for the pipeline to work as expected, you need to modify the `Jenkinsfile` to set your project ID.

Open the Jenkinsfile in your terminal editor, for example vi:
```
vi Jenkinsfile
```
Start the editor:
```
i
```
Add your `PROJECT_ID` to the `REPLACE_WITH_YOUR_PROJECT_ID` value. (Your `PROJECT_ID` is your GCP Project ID found in the `CONNECTION DETAILS` section of the lab—you can also run `gcloud config get-value project`) to find it:

```
def project = 'REPLACE_WITH_YOUR_PROJECT_ID'
def appName = 'gceme'
def feSvcName = "${appName}-frontend"
def imageTag = "gcr.io/${project}/${appName}:${env.BRANCH_NAME}.${env.BUILD_NUMBER}"
```

Save the Jenkinsfile file: hit Esc then (for vi users):
```
:wq
```

#### Modify the site
To demonstrate changing the application, we will change the gceme cards from blue to orange.

Open html.go:
```
vi html.go
```
Start the editor:
```
i
```
Change the two instances of `<div class="card blue">` with following:
```
<div class="card orange">
```
Save the html.go file: hit Esc then:
```
:wq
```
Open main.go:
```
vi main.go
```
Start the editor:
```
i
```
The version is defined in this line:
```
const version string = "1.0.0"
```
Update it to the following:
```
const version string = "2.0.0"
```
Save the main.go file one more time: Esc then:
```
:wq
```


### Kick off Deployment
Commit and push your changes:
```
git add Jenkinsfile html.go main.go

git commit -m "Version 2.0.0"

git push origin new-feature
```
This will kick off a build of your development environment.

After the change is pushed to the Git repository, navigate to the Jenkins user interface where you can see that your build started for the new-feature branch. It can take up to a minute for the changes to be picked up.


After the build is running, click the down arrow next to the build in the left navigation and select **Console output**:



Track the output of the build for a few minutes and watch for the `kubectl --namespace=new-feature apply...` messages to begin. Your new-feature branch will now be deployed to your cluster.

> Note: In a development scenario, you wouldn't use a public-facing load balancer. To help secure your application, you can use [kubectl proxy](http://kubernetes.io/docs/user-guide/connecting-to-applications-proxy/). The proxy authenticates itself with the Kubernetes API and proxies requests from your local machine to the service in the cluster without exposing your service to the Internet.



If you didn't see anything in Build Executor, not to worry. Just go to the Jenkins homepage --> sample app. Verify that the new-feature pipeline has been created.

Once that's all taken care of, start the proxy in the background:

```
kubectl proxy &
```


If it stalls, hit ctrl + x to exit out. Verify that your application is accessible by sending a request to localhost and letting kubectl proxy forward it to your service:
```
curl \
http://localhost:8001/api/v1/namespaces/new-feature/services/gceme-frontend:80/proxy/version
```
You should see it respond with 2.0.0, which is the version that is now running.

You have set up the development environment! Next, you will build on what you learned in the previous module by deploying a canary release to test out a new feature.


### Deploying a Canary Release
You have verified that your app is running the latest code in the development environment, so let's deploy that code to the canary environment.

Create a canary branch and push it to the Git server:
```
git checkout -b canary

git push origin canary
```
In Jenkins, you should see the canary pipeline has kicked off. Once complete, you can check the service URL to ensure that some of the traffic is being served by your new version. You should see about 1 in 5 requests (in no particular order) returning version 2.0.0.
```
export FRONTEND_SERVICE_IP=$(kubectl get -o \
jsonpath="{.status.loadBalancer.ingress[0].ip}" --namespace=production services gceme-frontend)
```
while true; do curl http://$FRONTEND_SERVICE_IP/version; sleep 1; done

If you keep seeing 1.0.0, try running the above commands again. Once you've verified that the above works, end the command with Ctrl-c.

That's it! You have deployed a canary release. Next you will deploy the new version to production.





### Deploying to production
Now that our canary release was successful and we haven't heard any customer complaints, deploy to the rest of your production fleet.

Create a canary branch and push it to the Git server:
```
git checkout master

git merge canary

git push origin master
```
In Jenkins, you should see the master pipeline has kicked off. Once complete, you can check the service URL to ensure that all of the traffic is being served by your new version, 2.0.0.

```
export FRONTEND_SERVICE_IP=$(kubectl get -o \
jsonpath="{.status.loadBalancer.ingress[0].ip}" --namespace=production services gceme-frontend)
```

```
while true; do curl http://$FRONTEND_SERVICE_IP/version; sleep 1; done
```

Once again, if you see instances of 1.0.0 try running the above commands again. You can stop this command by pressing Ctrl-c.

Example Output:
```
gcpstaging9854_student@qwiklabs-gcp-df93aba9e6ea114a:~/continuous-deployment-on-kubernetes/sample-app$ while true; do curl http://$FRONTEND_SERVICE_IP/version; sleep 1; done
2.0.0
2.0.0
2.0.0
2.0.0
2.0.0
2.0.0
^C

```

You can also navigate to site on which the gceme application displays the info cards. The card color changed from blue to orange. Here's the command again to get the external IP address so you can check it out:

```
kubectl get service gceme-frontend -n production
```



































---