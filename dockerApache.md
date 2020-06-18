# Data Engineering: Building A Data Platform
# What do we want to do?
- Twitter data to predict best time to post using the hashtag datascience or ai
- Find top tweets for the day
- Top users
- Analyze sentiment and keywords

# Tools
- [Docker](https://www.docker.com/)
- [Apache NiFi](https://nifi.apache.org/)
- [Apache Kafka](https://kafka.apache.org/)
- [Apache Zookeper](https://zookeeper.apache.org/)
- [Apache Zeppelin](https://zeppelin.apache.org/)

# Run Apache Nifi
`docker run --name nifi  -p 8080:8080 -d apache/nifi:latest`

# Run Apache Zookeeper
`docker run -d --name zookeeper-server      --network app-tier    -e  ALLOW_ANONYMOUS_LOGIN=yes     bitnami/zookeeper:latest`

# Run Apache Kafka
`docker run -d --name kafka-server      --network app-tier    -e  KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper-server:2181 -e ALLOW_PLAINTEXT_LISTENER=yes     bitnami/kafka:latest`

# Launch Kafka client instance after creating kafka topic
`docker run -it --rm    --network app-tier    -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper:2181    bitnami/kafka:latest kafka-topics.sh --create  --replication-factor 1 --partitions 1 --topic nifitopic    --zookeeper zookeeper-server:2181`

# Show version
`docker run -it --rm    --network app-tier    -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper:2181    bitnami/kafka:latest kafka-topics.sh --version    --zookeeper zookeeper-server:2181`

# List of Kafka Topics
`docker run -it --rm    --network app-tier    -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper:2181    bitnami/kafka:latest kafka-topics.sh --list    --zookeeper zookeeper-server:2181`

In the PublishKafkaRecord_2_0
Under properties, changed Kafka Brokers - `localhost:9092` to `Kafka-server:9092`

# Run Apache Zeppelin
`docker run -d -p 8081:8080 --rm \
-v /Users/xxxx/Documents/DockerFiles/logs:/logs \
-v /Users/xxxx/Documents/DockerFiles/Notebooks:/notebook \
-e ZEPPELIN_LOG_DIR='/logs' \
-e ZEPPELIN_NOTEBOOK_DIR='/notebook' \
--network app-tier --name zeppelin apache/zeppelin:0.7.3`