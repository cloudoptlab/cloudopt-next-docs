﻿﻿﻿Kafka is an open source flow processing platform developed by the Apache software foundation, written by Scala and Java. Kafka is a high-throughput distributed publishing subscription messaging system that handles all the action flow data on a consumer-sized web site. This movement (web browsing, search, and other user actions) is a crucial factor in many social functions on the modern web. These data are usually addressed by processing log and log aggregation due to throughput requirements. It is a viable solution for logging data and offline analysis systems like Hadoop, but also for real-time processing restrictions. Kafka's purpose is to unify online and offline message processing through the parallel loading mechanism of Hadoop, and to provide real-time consumption through clustering.

Cloudopt Next provides the plug-in for Kafka, which you only need to configure in the configuration file and start the plug-in.

Please refer to the corresponding dependency before use, add the version number yourself.

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-kafka</artifactId>
</dependency>
````

````json
net:
{
  "kafka": {
    "bootstrap.servers": "PLAINTEXT://127.0.0.1:9092",
    "key.deserializer": "org.apache.kafka.common.serialization.StringDeserializer",
    "value.deserializer": "org.apache.kafka.common.serialization.StringDeserializer",
    "key.serializer": "org.apache.kafka.common.serialization.StringSerializer",
    "value.serializer": "org.apache.kafka.common.serialization.StringSerializer",
    "acks": "1",
    "group.id": "net.cloudopt.next",
    "application.id": "service"
  }
}
````

````kotlin
fun main(args: Array<String>) {
    CloudoptServer.addPlugin(KafkaPlugin())
    CloudoptServer.run(TestCase::class)
}
````

````java
fun main(args: Array<String>) {
    CloudoptServer.addPlugin(KafkaPlugin());
    CloudoptServer.run(TestCase.class);
}
````

After the configuration is complete, information can be sent via KafkaManager.

````kotlin
KafkaManager.send(topic, key, value)
````

If any class fulfills the KafkaListener interface and places, the @autokafka annotation will automatically monitor the theme name set in @autokafka.

````kotlin
@AutoKafka("test-topic")
class TestKafka:KafkaListener {

    override fun listener(record: KafkaConsumerRecord<String, Any>) {
        println(record.topic())
        println(record.key())
        println(record.value())
    }

}
````

````java
@AutoKafka("test-topic")
public class TestKafka implements KafkaListener {

    @Override
    public void listener(@NotNull KafkaConsumerRecord<String, Object> record) {
        System.out.println(record.topic());
        System.out.println(record.key());
        System.out.println(record.value());
    }

}
````

> You can also set more settings in the configuration file. Please refer to Kafka official document for specific parameter names.

Above version 2.0.0, Kafka streams is supported. You only need to add "streams": "true" in the configuration file to automatically create links to Kafka streams. Because Kafka streams is dependent on Kafka, there is no special distinction between them in parameter settings. They are all set under the keyword Kafka.

