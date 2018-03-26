﻿﻿﻿﻿Kafka is an open source flow processing platform developed by the Apache software foundation, written by Scala and Java. Kafka is a high-throughput distributed publishing subscription messaging system that handles all the action flow data on a consumer-sized web site. This movement (web browsing, search, and other user actions) is a crucial factor in many social functions on the modern web. These data are usually addressed by processing log and log aggregation due to throughput requirements. It is a viable solution for logging data and offline analysis systems like Hadoop, but also for real-time processing restrictions. Kafka's purpose is to unify online and offline message processing through the parallel loading mechanism of Hadoop, and to provide real-time consumption through clustering.

Cloudopt Next provides the plug-in for Kafka, which you only need to configure in the configuration file and start the plug-in.

Please refer to the corresponding dependency before use. If you have not inherited the cloudopt-next parent, add the version number yourself.

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-kafka</artifactId>
</dependency>
````

````yaml
net:
  cloudopt:
    next:
      web:
        packageName: "net.cloudopt.next.kafka.test"
      kafka:
        servers: "PLAINTEXT://127.0.0.1:9092"
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
You can also make more Settings in the configuration file.

| Name     | Default| Description|
|:--------:|:---------|:-------|
| servers| ""| Kafka server address.      |
| keyDeserializer| "org.apache.kafka.common.serialization.StringDeserializer"| The de-serialization implementation class for Key.      |
| valueDeserializer| "org.apache.kafka.common.serialization.StringDeserializer"| The deserialization implementation class for Value.      |
| groupId| "cloudopt"| Consumer group that consumer belongs to.      |
| offsetRest| "earliest"| The operation is performed when the offset exceeds the reasonable range (out ofrange).      |
| autoCommit| "false"|If true, the last message offset already acquired by the Consumer is updated periodically in zk.      |
| keySerializer| "org.apache.kafka.common.serialization.StringSerializer"| Key's serialization implementation class.      |
| valueSerializer| "org.apache.kafka.common.serialization.StringSerializer"| The serialization implementation class of Value.      |
| acks| "1"| 0 indicates that the producer does not have to wait for the leader's confirmation, 1 indicates that the leader needs to confirm the local log written to it and immediately confirmed, and -1 indicates that all backups are completed and confirmed. Only for sync.      |

If you need to configure more things, you can set it directly through KafkaManager.config. Please refer to the official Kafka documentation for specific parameter names.


