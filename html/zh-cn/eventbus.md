## 什么是EventBus

Cloudopt Next是基于Vertx的，所以也支持Vertx的EventBus。

Vert.x应用程序是事件驱动，异步和单线程的。 Vert.x过程通过事件总线，这是Vert.x的事件驱动架构的内置一块通信。 结合异步处理，单线程组件和事件总线产生高度的可扩展性，并编写单线程应用对习惯于多线程并发Java的人来说是一种解脱。 可以说，Vert.x的最好的部分是其模块化的基于JVM的架构。 Vert.x应用程序可以运行在几乎所有的操作系统，并且可以使用任何支持的JVM兼容的编程语言来编写。 一个Vert.x应用可完全在单一语言编写，也可以是用不同的编程语言模块的跨界混搭。 Vert.x模块集成了Vert.x事件总线上。

每个Verticle的运行都是在Vertx.x的实例单线程中，通过Event Loop进行调度，而Verticle之间的相互调用和数据传递都是通过EventBus进行的。

我们不建议在非单机的情况下使用EventBus，请尽量使用消息队列。

## EventListener

在Cloudopt Next中使用仅需要实现EventListener并添加@AutoEvent注解，订阅指定事件。发布消息则是通过EventManager.send()或者EventManager.publish()。如果使用publish，所有订阅了该主题的监听器都会执行。

````kotlin
fun main(args: Array<String>) {
    CloudoptServer.addPlugin(EventPlugin())
    CloudoptServer.run(TestCase::class)
}
````

````kotlin
@AutoEvent("net.cloudopt.web.test")
class TestEventListener:EventListener {
    override fun listener(message: Message<Any>) {
        print(message.body())
    }
}
````

````kotlin
EventManager.send("net.cloudopt.web.test", "This is test message!")
````