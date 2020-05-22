## EventBus

Cloudopt Next是基于Vertx的，所以也支持Vertx的EventBus。

Vert.x应用程序是事件驱动，异步和单线程的。 Vert.x过程通过事件总线，这是Vert.x的事件驱动架构的内置一块通信。 结合异步处理，单线程组件和事件总线产生高度的可扩展性，并编写单线程应用对习惯于多线程并发Java的人来说是一种解脱。 可以说，Vert.x的最好的部分是其模块化的基于JVM的架构。 Vert.x应用程序可以运行在几乎所有的操作系统，并且可以使用任何支持的JVM兼容的编程语言来编写。 一个Vert.x应用可完全在单一语言编写，也可以是用不同的编程语言模块的跨界混搭。 Vert.x模块集成了Vert.x事件总线上。

每个Verticle的运行都是在Vertx.x的实例单线程中，通过Event Loop进行调度，而Verticle之间的相互调用和数据传递都是通过EventBus进行的。

我们不建议在非单机的情况下使用EventBus。

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

## Send Message

````kotlin
EventManager.send("net.cloudopt.web.test", "This is test message!")
EventManager.public("net.cloudopt.web.test", "This is test message!")
````

## After Event

其实我们在日常开发中经常会碰到调用完请求需要做些什么事情的场景，如新用户注册后需要给他发放优惠卷，在传统的开发模式下发放优惠券的代码是放在注册的代码后面。但是如果要再增加记录用户登录时间等功能的话，这个路由方法中的代码将会非常的多。

为了帮助大家在实际开发中进行解耦，我们提供了 `@afterEvent` 注解。Cloudopt Next 会自动在请求准备结束时调用 EventBus 的 send 方法进行发送，那么只需要让消费者订阅相应的事件就可以解耦了。

在使用这个注解前请先加载 `EventPlugin`。

````kotlin
@GET("afterEvent")
@AfterEvent(["net.cloudopt.web.test"])
fun afterEvent() {
    renderText("AfterEvent is success!")
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