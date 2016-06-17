Work in progress...

just a few docker notes:
=======================
on a Mac with docker-machine install create a kafka server running in docker:


docker pull spotify/kafka

docker run -p 0.0.0.0:9092:9092 -p 0.0.0.0:2081:2081 spotify/kafka

log in the running container and edit /opt/kafka_2.11-0.8.2.1/config/server.properties

change property advertised.host.name to advertised.host.name=localhost

docker restart<kafka server>


for local access on mac:
----------------
docker-machine ssh default -L 9092:<docker-machine ip>:9092
docker-machine ssh default -L 2181:<docker-machine ip>:2181


prepare topic
-------------
docker exec -it dd1c /opt/kafka_2.11-0.8.2.1/bin/kafka-topics.sh --create --topic carts --partitions 1 --replication-factor 1 --zookeeper <docker-machine ip>:2181

docker exec -it dd1c /opt/kafka_2.11-0.8.2.1/bin/kafka-topics.sh --list --zookeeper <docker-machine ip>:2181

test topic:
-----------
docker exec -it dd1c /opt/kafka_2.11-0.8.2.1/bin/kafka-console.consumer.sh --zookeeper <docker-machine ip>:2181 --topic carts
docker exec -it dd1c /opt/kafka_2.11-0.8.2.1/bin/kafka-console-producer.sh --broker-list <docker-machine ip>:9092 --topic carts