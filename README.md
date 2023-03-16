# kafka-streams-status-statistic
POC for Kafka Stream research

Learn more at https://kafka.apache.org/34/documentation/streams/quickstart

1. Start zookeeper

bin/zookeeper-server-start.sh config/zookeeper.properties

2. Start kafka

bin/kafka-server-start.sh config/server.properties
Note: skip step 1 and 2 if use Kafka of TestOps

3. Craete input and output topic

bin/kafka-topics.sh --create \
    --bootstrap-server localhost:9092 \
    --replication-factor 1 \
    --partitions 1 \
    --topic tracking-topic
    
bin/kafka-topics.sh --create \
    --bootstrap-server localhost:9092 \
    --replication-factor 1 \
    --partitions 1 \
    --topic analytics-topic
    
4. Start terminal to follow input and ouput topics

bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 \
    --topic tracking-topic \
    --from-beginning \
    --formatter kafka.tools.DefaultMessageFormatter \
    --property print.key=true \
    --property print.value=true \
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    --property value.deserializer=org.apache.kafka.common.serialization.StringDeserializer

bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 \
    --topic analytics-topic \
    --from-beginning \
    --formatter kafka.tools.DefaultMessageFormatter \
    --property print.key=true \
    --property print.value=true \
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    
5. Start TestOps and this program
6. Create tag and assign Jira issue
