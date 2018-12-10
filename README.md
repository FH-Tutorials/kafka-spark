# kafka-spark


## Pre-Install

  * docker & docker-compose
  * git
  * tar/wget [for Linux]
  * 7zip [for Windows]

## Install

Get latest kafka version from the official [Download Page](https://www.apache.org/dyn/closer.cgi?path=/kafka/2.1.0/kafka_2.11-2.1.0.tgz) and unzip it. E.g. on Linux

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

From the logs of docker you can find the login token necessary for the jupyter login. Execute

```bash
docker logs $(docker ps -f name=notebook -q)
```

from Powershell or Bash. In the logs the following line should be found:

> "Copy/paste this URL into your browser when you connect for the first time, to login with a token:"

Beneath the login token is presented like:

> http://(bce2f8d711eb or 127.0.0.1):8888/?token=cddf0aaf8cefe270ff318973c0dd382c957917fa7ea8e5bd

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
