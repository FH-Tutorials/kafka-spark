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


```bash
# create new topic
kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
```
