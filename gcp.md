---
layout: page
title: Google Cloud Platform
---



## Regions and Zones [^rz]

[^rz]: [Regions and Zones](https://cloud.google.com/compute/docs/regions-zones/)

Region | Zones | Location
------------ | ------------- | ------------
asia-east1 | a, b, c | Changhua County, Taiwan
asia-east2 | a, b, c | Hong Kong
asia-northeast1 | a, b, c | Tokyo, Japan
asia-northeast2 | a, b, c | Osaka, Japan
asia-south1 | a, b, c | Mumbai, India
asia-southeast1 | a, b, c | Jurong West, Singapore
australia-southeast1 | a, b, c | Sydney, Australia
europe-north1 | a, b, c | Hamina, Finland
europe-west1 | b, c, d | St. Ghislain, Belgium
europe-west2 | a, b, c | London, England, UK
europe-west3 | a, b, c | Frankfurt, Germany
europe-west4 | a, b, c | Eemshaven, Netherlands
europe-west6 | a, b, c | Zürich, Switzerland
northamerica-northeast1 | a, b, c | Montréal, Québec, Canada
southamerica-east1 | a, b, c | Osasco (São Paulo), Brazil
us-central1 | a, b, c, f | Council Bluffs, Iowa, USA
us-east1 | b, c, d | Moncks Corner, South Carolina, USA
us-east4 | a, b, c | Ashburn, Northern Virginia, USA
us-west1 | a, b, c | The Dalles, Oregon, USA
us-west2 | a, b, c | Los Angeles, California, USA


### Setting a default compute zone

```bash
gcloud config set compute/zone us-central1-a
```

### Set the default region:

```bash
gcloud config set compute/region us-central1
```


## `gsutil` command line

-[ ] TODO

## VM instances

### Help
```bash
gcloud compute instances create --help
```

### Create 
```bash
gcloud compute instances create gcelab2 --machine-type n1-standard-2 --zone us-central1-c
```

### List
```bash
gcloud compute instances list
```

### SSH access
```bash
gcloud compute ssh gcelab2 --zone us-central1-c

```

### Template

**Create a startup script to be used by every virtual machine instance.**

```bash
cat << EOF > startup.sh
#! /bin/bash
apt-get update
apt-get install -y nginx
service nginx start
sed -i -- 's/nginx/Google Cloud Platform - '"\$HOSTNAME"'/' /var/www/html/index.nginx-debian.html
EOF
```



#### Create template

```bash
gcloud compute instance-templates create nginx-template \
         --metadata-from-file startup-script=startup.sh
```

### Target pool

```bash
gcloud compute target-pools create nginx-pool
```


### Instance group

```bash

gcloud compute instance-groups managed create nginx-group \
         --base-instance-name nginx \
         --size 2 \
         --template nginx-template \
         --target-pool nginx-pool

```

### Firewall rules

#### Create

```bash
gcloud compute firewall-rules create www-firewall --allow tcp:80
```

```bash
gcloud compute forwarding-rules create nginx-lb \
         --region us-central1 \
         --ports=80 \
         --target-pool nginx-pool
```

#### List rules

```bash

gcloud compute forwarding-rules list
```

---


## Kubernetes

### Kubernetes Engine cluster

#### Create cluster

```bash
gcloud container clusters create [CLUSTER-NAME]
# like
gcloud container clusters create cluster1

```

#### List cluster

```bash
gcloud container clusters list
```


#### Get authentication credentials for the cluster

```bash
gcloud container clusters get-credentials [CLUSTER-NAME]
# like
gcloud container clusters get-credentials cluster1

```

#### Deploy application

##### Deploy

```bash
kubectl run hello-server --image=gcr.io/google-samples/hello-app:1.0 --port 8080
```

##### Expose your application to external traffic

```bash
kubectl expose deployment hello-server --type="LoadBalancer"
```

##### After deploy - get service detail

```bash
kubectl get service hello-server
```

##### Distroy cluster

```bash
gcloud container clusters delete cluster1
```

#### kubectl

##### check version
```bash
kubectl version
```

##### run instance
```bash
kubectl run nginx --image=nginx:1.10.0
```


##### get pots

```bash
kubectl get pods
```

##### expose deployment
```bash

kubectl expose deployment nginx --port 80 --type LoadBalancer
```

##### get services

```bash
kubectl get services
```

##### scale deployment

```bash
kubectl scale deployment nginx --replicas 3
```

--

## App engine

### deploy

```bash
gcloud app deploy ./index.yaml ./app.yaml
```

--

## Storage

- [ ] to add

-- 

## Deployment Manager and Stackdriver


### `yaml` file
```yaml
resources:
  - name: my-vm
    type: compute.v1.instance
    properties:
      zone: us-central1-a
      machineType: zones/ZONE/machineTypes/n1-standard-1
      metadata:
        items:
        - key: startup-script
          value: "apt-get update"
      disks:
      - deviceName: boot
        type: PERSISTENT
        boot: true
        autoDelete: true
        initializeParams:
          sourceImage: https://www.googleapis.com/compute/v1/projects/debian-cloud/global/images/debian-9-stretch-v20180806
      networkInterfaces:
      - network: https://www.googleapis.com/compute/v1/projects/PROJECT_ID/global/networks/default
        accessConfigs:
        - name: External NAT
          type: ONE_TO_ONE_NAT
```

### create deployment
```bash
gcloud deployment-manager deployments create my-first-depl --config mydeploy.yaml
```
### update deployment
```bash
gcloud deployment-manager deployments update my-first-depl --config mydeploy.yaml
```

---