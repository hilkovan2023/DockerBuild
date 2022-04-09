# Docker run command

### 1.consul
docker run --name consul -v /home/yangxk/workspace/Docker/consul/data:/data -v /home/yangxk/workspace/Docker/consul/conf:/config --restart=always -p 8300:8300 -p 8301:8301 -p 8302:8302 -p 8400:8400 -p 8500:8500 consul agent -server -bootstrap-expect 1 -ui -bind=0.0.0.0 -client=0.0.0.0

### 2.rabbitmq
docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 -v /home/yangxk/workspace/Docker/rabbitmq/data:/var/lib/rabbitmq --hostname myRabbit -e RABBITMQ_DEFAULT_USER=root -e RABBITMQ_DEFAULT_PASS=yang13589392653 rabbitmq

### 3.emqx/emqx
docker run --name emqx -p 18083:18083 -p 1883:1883 -p 8084:8084 -p 8883:8883 -p 8083:8083 -d emqx/emqx

### 4.zookeeper
docker run --name zookeeper -p 2181:2181 -v /home/yangxk/workspace/Docker/zookeeper/conf:/etc/zookeeper/conf -v /home/yangxk/workspace/Docker/zookeeper/data:/data -v /home/yangxk/workspace/Docker/zookeeper/logs:/etc/zookeeper/log -d --restart=always zookeeper

### 5.kafka(需要配合zookeeper）
docker run  -d --name kafka --add-host kafka:192.168.230.129 --link zookeeper -p 9092:9092 -e KAFKA_BROKER_ID=0 -e KAFKA_ZOOKEEPER_CONNECT=192.168.230.129:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://192.168.230.129:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -t wurstmeister/kafka

----(测试kafka)
#### 进入kafka的bash窗口
    docker exec -it kafka /bin/bash
#### 生产者创建topic
    kafka-console-producer.sh --broker-list localhost:9092 --topic topicname
#### 消费者消费topic
    kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topicname --from-beginning
----
