Kafka是由Apache软件基金会开发的一个开源流处理平台，由Scala和Java编写。Kafka是一种高吞吐量的分布式发布订阅消息系统，它可以处理消费者规模的网站中的所有动作流数据。 这种动作（网页浏览，搜索和其他用户的行动）是在现代网络上的许多社会功能的一个关键因素。 这些数据通常是由于吞吐量的要求而通过处理日志和日志聚合来解决。 对于像Hadoop的一样的日志数据和离线分析系统，但又要求实时处理的限制，这是一个可行的解决方案。Kafka的目的是通过Hadoop的并行加载机制来统一线上和离线的消息处理，也是为了通过集群来提供实时的消费。

Cloudopt Next为Kafka提供了插件，您只需要在配置文件中配置后并启动插件既可。

在使用前请先自行引用相应的依赖。如果您并没有继承cloudopt-next-parent的话，请自行添加版本号。

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
您还可以在配置文件中进行更多设置。

| Name     | Default| Description|
|:--------:|:---------|:-------|
| servers| ""| Kafka服务器地址。      |
| keyDeserializer| "org.apache.kafka.common.serialization.StringDeserializer"| Key的反序列化实现类。      |
| valueDeserializer| "org.apache.kafka.common.serialization.StringDeserializer"| Value的反序列化实现类。      |
| groupId| "cloudopt"| consumer所属的consumer group。      |
| offsetRest| "earliest"| 当发现offset超出合理范围（out ofrange)时进行的操作。      |
| autoCommit| "false"| 如果是true,定期向zk中更新Consumer已经获取的last message offset。      |
| keySerializer| "org.apache.kafka.common.serialization.StringSerializer"| Key的序列化实现类。      |
| valueSerializer| "org.apache.kafka.common.serialization.StringSerializer"| Value的序列化实现类。      |
| acks| "1"| 0表示producer无须等待leader的确认，1代表需要leader确认写入它的本地log并立即确认，-1代表所有的备份都完成后确认。仅仅for sync。      |

如果您需要配置更多东西，您可以直接通过KafkaManager.config进行配置，具体参数名请参考Kafka官方文档。