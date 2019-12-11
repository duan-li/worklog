---
layout: post
title: Cloud infrastructure
date: 2019-12-11 00:11 +0000
---

## Core

```mermaid
graph TB
A[Request Fulfillment] ==> B[Storage]
A[Request Fulfillment] ==> C[Data Persistence]
```

### Request Fulfillment
 
Could be 
 - Application engine
 - VM
 - Serverless
 - Server
 - Service

### Storage

Store file or object. 

### Data Persistence
 - Relation DB
 - Document DB


---

## Traffic

```mermaid
graph TB
LB((Load Balance)) --> C(Cache)
C(Cache) --> RF[Request Fulfillment]
RF[Request Fulfillment] ==> C2(Cache)
C2(Cache) ==> S[Storage]
RF[Request Fulfillment] ==> C3(Cache)
C3(Cache) ==> DP[Data Persistence]
RF[Request Fulfillment] --> Q{Queue}
```

### Load balance

See [load balance](/2019/12/11/load-balance.html)

### Cache
 - redis
 - memcache

### Queue
 - redis
 - kafka

