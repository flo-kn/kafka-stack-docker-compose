# Spin up 2 Kafkas witha an MM2 Environment

docker-compose -f zk-2-single-kafka-2-single-mm.yml up | grep mirrormaker


### Produce

Go into one of the Kafkas
```sh
docker exec -it kafka2 /bin/bash
```

export the topic name
```sh
export TOPIC_NAME=the-topic-2-B-synced
```

list topic
```sh
kafka-console-producer --broker-list localhost:9092 --topic $TOPIC_NAME
```

create topic
```sh
docker exec -it kafka1 kafka-topics --create --topic $TOPIC_NAME --partitions 1 --replication-factor 1 --if-not-exists --bootstrap-server localhost:9092
```

enter the container
```sh
docker exec -it kafka1 /bin/bash
```

```sh
kafka-console-consumer --bootstrap-server kafka2:9092 --topic $TOPIC_NAME
```
