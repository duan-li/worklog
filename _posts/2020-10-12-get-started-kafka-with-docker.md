---
layout: post
title: Get started Kafka with Docker
date: 2020-10-11 05:37 +0000
---

## Zookeeper [^docker_zookeeper]

[^docker_zookeeper]: [bitnami/zookeeper](https://hub.docker.com/r/bitnami/zookeeper/)

```bash
docker run -it --rm \
    -e ALLOW_ANONYMOUS_LOGIN=yes \
    -p 2181:2181 \
    -p 2888:2888 \
    -p 3888:3888 \
    -p 8080:8080 \
    -v /tmp/host/zookeeper:/bitnami/zookeeper
    bitnami/zookeeper
```

## Kafka [^docker_kafka]

[^docker_kafka]: [bitnami/kafka](https://hub.docker.com/r/bitnami/kafka/)

```bash
docker run -it --rm \
    -p 9092:9092 \
    -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://127.0.0.1:9092 \
    -e KAFKA_LISTENERS=PLAINTEXT://:9092 \
    -e KAFKA_ZOOKEEPER_CONNECT=127.0.0.1:2181 \
    -e ALLOW_PLAINTEXT_LISTENER=yes \
    -v /tmp/host/kafka:/bitnami/kafka
    bitnami/kafka
```


## Testing [^demo]

[^demo]: [Kafka and Zookeeper with Docker](https://medium.com/rahasak/kafka-and-zookeeper-with-docker-65cff2c2c34f)

`ches/kafka` can provide tools[^demo_docker]. And source code is in github[^dockerfile]. 

[^demo_docker]: [ches/kafka](https://hub.docker.com/r/ches/kafka/)

[^dockerfile]: [ches/docker-kafka](https://github.com/ches/docker-kafka)

### Create topic

```bash
docker run \
--rm ches/kafka kafka-topics.sh \
--create \
--topic test_topic \
--replication-factor 1 \
--partitions 1 \
--zookeeper 127.0.0.1:2181
```

### List topic

```bash
docker run \
--rm ches/kafka kafka-topics.sh \
--list \
--zookeeper 127.0.0.1:2181
```

### producer

```bash
docker run --rm --interactive \
ches/kafka kafka-console-producer.sh \
--topic test_topic \
--broker-list 127.0.0.1:9092
```


### consumer

```bash
docker run --rm \
ches/kafka kafka-console-consumer.sh \
--topic test_topic \
--from-beginning \
--zookeeper 127.0.0.1:2181
```

