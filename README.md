# kafka-basic-test





Run single node of kafka
```sh
docker compose -f kafka-single-node.yml up -d
```


## Kafka Commands

Logging into the Kafka Container
```sh
docker exec -it kafka-broker /bin/bash
```

Navigate to the Kafka Scripts directory
```sh
cd /opt/bitnami/kafka/bin
```

Creating new Topics
```sh
./kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --create \
    --topic kafka.learning.one \
    --partitions 1 \
    --replication-factor 1
```
        
Listing Topics
```sh
./kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --list
```

Getting details about a Topic
```sh
./kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --describe
```

Publishing Messages to Topics
```sh
./kafka-console-producer.sh \
    --bootstrap-server localhost:29092 \
    --topic kafka.learning.one
```

Consuming Messages from Topics
```sh
./kafka-console-consumer.sh \
    --bootstrap-server localhost:29092 \
    --topic kafka.learning.one \
    --from-beginning
```

Deleting Topics
```sh
./kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --delete \
    --topic kafka.learning.one
```

Create a Topic with multiple partitions
```sh
./kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --create \
    --topic kafka.learning.two \
    --partitions 3 \
    --replication-factor 1
```
        
Check topic partitioning
```sh
./kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --topic kafka.learning.two \
    --describe
```

Publishing Messages to Topics with keys
```sh
./kafka-console-producer.sh \
    --bootstrap-server localhost:29092 \
    --property "parse.key=true" \
    --property "key.separator=:" \
    --topic kafka.learning.two
```

Consume messages using a consumer group
```sh
./kafka-console-consumer.sh \
    --bootstrap-server localhost:29092 \
    --topic kafka.learning.two \
    --group test-consumer-group \
    --property print.key=true \
    --property key.separator=" = " \
    --from-beginning
```

Check current status of offsets
```sh
./kafka-consumer-groups.sh \
    --bootstrap-server localhost:29092 \
    --describe \
    --all-groups
```
