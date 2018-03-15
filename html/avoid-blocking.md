As we mentioned before, Cloudopt Next is based on Vertx, and Vertx is a framework similar to NodeJs. It handles network requests through an event loop. So Vertx does not recommend blocking threads, such as database operations are too slow, as much as possible through asynchronous operations. If it is impossible to avoid blocking, use Worker.

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

You can put blocked code into the Worker and run it.If you put the methods of the Render series together in the Resource class, Worker will automatically change this request from single-threaded to concurrent.