# kafka-spark

Quick installation manual for a docker-compose cluster including [Apache Kafka](https://kafka.apache.org/) managed by [Apache Zokeeper](https://zookeeper.apache.org/) as well as a [Apache Spark](https://spark.apache.org/) image together with a [jupyter notebook](https://jupyter.org/).

## Pre-Install

  * docker & docker-compose
  * git
  * get tar/gzip utility. E.g.:
    * 7zip [for Windows]
    * tar [for Linux]

## Install

Get latest kafka version from the official [Download Page](https://www.apache.org/dyn/closer.cgi?path=/kafka/2.1.0/kafka_2.11-2.1.0.tgz) and unzip it. E.g. on Linux

```bash
wget http://ftp.halifax.rwth-aachen.de/apache/kafka/2.1.0/kafka_2.11-2.1.0.tgz
tar -xvzf kafka_2.11-2.1.0.tgz
```

Fix the kafka_dir parameter in the docker-composer.yml to the directory name of the extracted kafka binaries, in case it is different. **Caution**: The extraction directory for the kafka files should lay within the repository folder. Docker can only copy files which are within the directroy of docker-compose.yml. Next build the docker containers using compose:

```bash
docker-compose build
```

Finally run the container cluster by calling

```bash
docker-compose up
```

From the logs docker keeps during runtime, you can find the login token necessary for the jupyter login. Execute

```bash
docker logs $(docker ps -f name=notebook -q)
```

from Powershell or Bash. When following the log entries the following line should be printed somewhere:

> "Copy/paste this URL into your browser when you connect for the first time, to login with a token:"

Beneath the login token is presented together with the URL like:

> http://(bce2f8d711eb or 127.0.0.1):8888/?token=cddf0aaf8cefe270ff318973c0dd382c957917fa7ea8e5bd

Thus, depending on the IP of your docker machine (usually its localhost) you can reach the notebook with:

> http://[docker machine IP]:8888/?token=cddf0aaf8cefe270ff318973c0dd382c957917fa7ea8e5bd

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
bin\windows\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

# list topics
bin\windows\kafka-topics.bat --list --zookeeper localhost:2181

# produce ...
bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic test

# consume ...
bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test --from-beginning
```

## Further Help & FAQ

Further help can be found at the [Kafka Quickstart Tutorial](https://kafka.apache.org/quickstart) as well as on the [Kafka Documentation Website](https://kafka.apache.org/). Next you'll find some common problems and how to solve them.

- [Eduroam Wifi Problems](#eduroam-wifi-problems)
- [Weird error messages](#weird-error-messages)
- [docker-compose build fails](#docker-compose-build-fails)
- [No entry found for connection](#no-entry-found-for-connection)

### Eduroam Wifi Problems

In some cases the cluster fails to start because it seems that there is an issue with the firewall. Thus, it might be necessary to add an DNS entry into the docker-compose.yml file which is described [here](https://docs.docker.com/compose/compose-file/#dns) and can be found using `ipconfig /all` on windows and e.g. `cat /etc/resolv.conf` on Linux.

### Weird error messages

In special cases (particular on Windows) there are strange errors, often related to network connections, which happens sometimes e.g. when the computer came back from hibernation. That means that the docker daemon might be in an  inconsistent state, where usually a restart of the daemon solves the problem.

## docker-compose build fails

The building using docker-compose fails with the error message: "ERROR: Service 'zookeeper' failed to build: COPY failed: stat ...". In that case the downloaded Kafka binaries are in the wrong directory. The extraction directory for the kafka files should lay within the repository folder. Docker can only copy files which are within the directroy of docker-compose.yml

## No entry found for connection

It may occure, when running a consumer or a producer that you receive the error "No entry found for connection <number>". In that case you need to add an entry into the **hosts** file for kafka and zookeeper referencing 127.0.0.1. Details on how to do that you can read about at the Java [Producer/Cosumer Example](https://github.com/FH-Tutorials/KafkaProducerConsumer#before-running-the-start-scripts).
