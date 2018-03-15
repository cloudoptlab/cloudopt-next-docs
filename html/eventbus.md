## What is an EventBus

Cloudopt Next is based on Vertx, so it also supports Vertx's EventBus.

Vert.x applications are event-driven, asynchronous and single-threaded. The Vert.x process passes through the event bus, which is a built-in communication for Vert.x's event-driven architecture. Combined with asynchronous processing, single-threaded components and event buses produce a high degree of scalability, and writing single-threaded applications is a relief for people accustomed to multi-threaded concurrent Java. It can be said that the best part of Vert.x is its modular JVM-based architecture. Vert.x applications can run on almost any operating system and can be written using any supported JVM-compatible programming language. A Vert.x application can be written entirely in a single language, or it can be a cross-premises mashup with different programming language modules. The Vert.x module integrates the Vert.x event bus.

Each verticle is run in a single thread of the Vertx.x instance, dispatched through the Event Loop, and the reciprocal calls and data transfer between the verticles are performed through EventBus.

We do not recommend using EventBus in non-standalone situations. Use message queues whenever possible.

## EventListener

Using it in Cloudopt-Next only requires implementing EventListener and adding @AutoEvent annotations to subscribe to specific events. Posting a message is via EventManager.send() or EventManager.publish(). If publish is used, all listeners that subscribe to the topic will execute.

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