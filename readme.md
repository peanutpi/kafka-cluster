# Kafka Cluster using docker

To provision a multi-broker kafka cluster using **docker**.

## Start kafka single node setup

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
```

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
```

## Destroy kafka single node setup

```
docker-compose down
```

- all the data will be saved on mounted directory `kafkaData` & `zookeeperData` so in case you restart the whole data your previous data will be available even after restart or destroy.