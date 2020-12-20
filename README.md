# ProducerConsumerWithKafka
Producuer and Consumer app by using Apache Kafka and Zookeper

Docker

The first thing you need is to pull down the latest Docker images of both Zookeeper and Kafka

# Zookeeper
docker pull confluentinc/cp-zookeeper

# Kafka
docker pull confluentinc/cp-kafka

Before we create any contains, first create a new network that both contains are going to use.

docker network create kafka

Now you can create both Zookeeper and Kafka containers. Kafka needs to communicate with Zookeeper. 
All the port mappings are the standard ports listed in the Zookeeper and Kafka docs.

# Zookeeper
docker run -d --network=kafka --name=zookeeper -e ZOOKEEPER_CLIENT_PORT=2181 -e ZOOKEEPER_TICK_TIME=2000 -p 2181:2181  confluentinc/cp-zookeeper

# Kafka
docker run -d --network=kafka --name=kafka -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092 -p 9092:9092  confluentinc/cp-kafka

# Create or List Topic 

docker exec -it <zookeeper_container_id> kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic testLogs

docker exec -it <zookeeper_container_id> kafka-topics --list --zookeeper localhost:2181 


# GUI Tool for Apache Kafka
“Kafka Tool” : http://www.kafkatool.com/
"Conduktor" : https://www.conduktor.io
