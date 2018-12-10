# kafka-spark


## Pre-Install

  * docker & docker-compose
  * git

## Install

Download latest kafka version and unzip it. E.g.

```bash
wget http://ftp.halifax.rwth-aachen.de/apache/kafka/2.1.0/kafka_2.11-2.1.0.tgz
tar -xvzf kafka_2.11-2.1.0.tgz
```

Fix the kafka_dir parameter in the docker-composer.yml to the directory name of the extracted kafka binaries, in case it is different. Then build the docker container:

```bash
docker-compose build
```

Finally run the container by calling

```bash
docker-compose up
```

## Important Commands

Executed from kafka main directory:

**For Linux**

```bash
# create new topic
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

# list topics
bin/kafka-topics.sh --list --zookeeper localhost:2181

# produce ...
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test

# consume ...
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
```

**For Windows**

```powershell
# create new topic
bin/windows/kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

# list topics
bin/windows/kafka-topics.bat --list --zookeeper localhost:2181

# produce ...
bin/windows/kafka-console-producer.bat --broker-list localhost:9092 --topic test

# consume ...
bin/windows/kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test --from-beginning
```

## Further Help

Further help can be found at the [Kafka Documentation](https://kafka.apache.org/quickstart)