# Kafka Cluster using docker

To provision a multi-broker kafka cluster using **docker**.

## Start kafka multi node setup

- Run following command from the root directory

```
docker-compose up -d
```

## Create topic using kafka cli 

- verify that we are able to create a topic using kafka cli & after that listing all the available topics.

``` 
$> bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
Created topic "test".

$> bin/kafka-topics.sh --list --zookeeper localhost:2181
test

$> bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic test
Topic:test	PartitionCount:1	ReplicationFactor:2	Configs:
	Topic: test	Partition: 0	Leader: 2	Replicas: 2,1	Isr: 2,1
```

- Here we are able to see that our topic is in sync with 2 nodes with broker id 1 & 2.

## Produce test message 
 
- verify by starting a producer & consumer that we are able to send & receive message using kafka cli

```
$> bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
Hi
Hello
ABc
^C
$> bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
hi
hello
good morning
^CProcessed a total of 3 messages

// Even you can receive messages from other node.
$> bin/kafka-console-consumer.sh --bootstrap-server localhost:9093 --topic test --from-beginning
hi
hello
good morning
^CProcessed a total of 3 messages
```


## Destroy kafka single node setup

```
docker-compose down
```

- all the data will be saved on mounted directory `kafkaData` & `zookeeperData` so in case you restart the whole data your previous data will be available even after restart or destroy.

## Reference

- [Apache Kafka Quick Start](http://kafka.apache.org/quickstart)