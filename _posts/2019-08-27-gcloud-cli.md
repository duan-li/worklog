---
layout: post
title: gcloud cli
date: 2019-08-27 13:30 +0000
---



## Before start

Setup `project id` and `zone` [^zone]

[^zone]: [Regions and Zones](https://cloud.google.com/compute/docs/regions-zones/)

```bash
export PROJECT_ID=<project-id>
export ZONE=<zone-code>
```


## Project
Check current project `gcloud compute project-info describe --project <project-id>`


### Virtual machine

#### Create VM

```bash
gcloud compute instances create gcelab2 --machine-type n1-standard-2 --zone $ZONE
```

Get more help.

```bash
gcloud compute instances create --help
```

#### List VM

```bash
gcloud compute instances list
```

#### VM detail
```bash
gcloud compute instances describe <your_vm>
```

#### Access VM instance
Access VM via `ssh`.
```bash
gcloud compute ssh <your_vm> --zone $ZONE
```


## `gcloud` commands

```bash
gcloud -h
```

Output:
```bash
Usage: gcloud [optional flags] <group | command>
  group may be           access-context-manager | ai-platform | alpha | app |
                         asset | auth | beta | bigtable | builds | components |
                         composer | compute | config | container | dataflow |
                         dataproc | datastore | debug | deployment-manager |
                         dns | domains | endpoints | filestore | firebase |
                         functions | iam | iot | kms | logging | ml |
                         ml-engine | organizations | projects | pubsub | redis |
                         resource-manager | scheduler | services | source |
                         spanner | sql | tasks | topic
  command may be         docker | feedback | help | info | init | version

For detailed information on this command and its flags, run:
  gcloud --help
```

### config


```bash
gcloud config --help

gcloud help config
```

#### List config 

```bash
gcloud config list
gcloud config list --all

```

#### List components

```bash
gcloud components list
```

#### Install components

Install `beta`.
```bash
gcloud components install beta
```

Start to using `beta`, bottom bar.
```bash
gcloud beta interactive
```




---
