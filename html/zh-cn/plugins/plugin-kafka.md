Kafka是由Apache软件基金会开发的一个开源流处理平台，由Scala和Java编写。Kafka是一种高吞吐量的分布式发布订阅消息系统，它可以处理消费者规模的网站中的所有动作流数据。 这种动作（网页浏览，搜索和其他用户的行动）是在现代网络上的许多社会功能的一个关键因素。 这些数据通常是由于吞吐量的要求而通过处理日志和日志聚合来解决。 对于像Hadoop的一样的日志数据和离线分析系统，但又要求实时处理的限制，这是一个可行的解决方案。Kafka的目的是通过Hadoop的并行加载机制来统一线上和离线的消息处理，也是为了通过集群来提供实时的消费。

Cloudopt Next为Kafka提供了插件，您只需要在配置文件中配置后并启动插件既可。

在使用前请先自行引用相应的依赖，请自行添加版本号。

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-kafka</artifactId>
</dependency>
````

````json
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

配置完成后可以通过KafkaManager发送信息。

````kotlin
KafkaManager.send(topic, key, value)
````

任意一个类只要实现了KafkaListener接口并放置了@AutoKafka注解，就会自动监听@AutoKafka中设置的主题名。

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
> 您还可以在配置文件中进行更多设置，具体参数名请参考Kafka官方文档。

在 2.0.0 版本以上，支持 Kafka Streams，你只需要在配置文件中增加 "streams": "true", 便会自动创建 Kafka Streams 的链接。因为 Kafka Streams 是依赖 Kafka 的，所以在参数设置就没有特地将两者区分开来，都是在关键字 kafka 下设置。