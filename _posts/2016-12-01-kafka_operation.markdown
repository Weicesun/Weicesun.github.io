---
layout: post
title:  "Kafka basic operation"
date:   2016-12-01 +0800
categories: course
---

# Kafka basic operation incase I forget

## I finally decide where to work. In class I try to use kafka to pipe data into spark engine. I write this blog to prevent me from forgetting.

Kafka is pub sub log message system. It is wildly used in distributed system because it has really high throughput and is highly reliable.

## Start zookeeper

Different broker need zookeeper to help elect leader
```
 bin/zookeeper-server-start.sh config/zookeeper.properties

```

## Start a kafka broker

```
 bin/kafka-server-start.sh config/server.properties

```
If you want to start many broker, you need write different properties file.

## Create a topic

```
 bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 
--partitions 1 --topic topic-name

```

## Start producer and consumer

We need to mention topic when we setup producer and consumer.
```
 bin/kafka-console-producer.sh --broker-list localhost:9092 --topic topicname
 bin/kafka-console-consumer.sh --zookeeper localhost:2181 —topic topicname 
--from-beginning
```

In my project I need to program to have data sourcer to be my producer and spark engine to be my consumer.


