前面讲过Cloudopt Next是基于Vertx的，而Vertx是一个类似NodeJs的框架，通过事件循环完成对网络请求的处理。所以Vertx不建议阻塞线程，例如数据库操作太慢等情况，尽可能通过异步进行操作。如果不可能避免的需要阻塞，请使用Worker。

````kotlin
Worker.worker<Any>(Handler<Future<Any>>{ f ->
    renderText("success!")
}, Handler<AsyncResult<Any>>{ result ->

})
````

````java
Worker.INSTANCE.worker(f -> {
    renderText("success!");
}, result -> {

});
````

您可以将会阻塞的代码放入worker中运行，如果您在Resource类下将render系列的方法一并放入，Worker将自动将这个请求从单线程变成并发。

有时候很难避免bloing的情况下，您可以在路由的方法上增加@Blocking注解，使其自动变为普通的路由。

````kotlin
@Blocking
@GET("blocking")
fun blocking() {
    renderText("This is Blocking!")
}
````

````java
@Blocking
@GET("blocking")
public void blocking() {
    renderText("This is Blocking!")
}
````