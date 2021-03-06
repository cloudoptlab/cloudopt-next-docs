﻿Cloudopt-next-redis is a Redis Plugin ported to JFinal. Using RedisPlugin, you can use Redis exceptionally conveniently. The plugin provides not only rich API but also supports multiple Redis servers. Redis has high performance, rich data structure, and natural support for data persistence. It is a widely used Nosql database. Effective application of Redis can greatly improve system performance and save hardware costs.

Please refer to the appropriate dependencies before use, please add the version number yourself.

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-redis</artifactId>
</dependency>
````

##Configuration

Cloudopt-next-redis also supports automatic reading of configuration files.

````json
{
  "redis": {
    "host": "localhost",
    "port": 6379,
    "timeout": 3000,
    "password": "",
    "database": 0
  }
}
````

All parameters are not required. The default host is localhost and the port is 6379.

## Startup

After the configuration is complete, you need to start the plug-in before the server starts.

````kotlin
fun main(args: Array<String>) {
    CloudoptServer.addPlugin(RedisPlugin())
    CloudoptServer.run(TestCase::class)
}
````

````java
fun main(args: Array<String>) {
    CloudoptServer.addPlugin(RedisPlugin());
    CloudoptServer.run(TestCase.class);
}
````

## Cache

Redis and Cache together can be very convenient to use Redis services, Redis objects through the use () method to get the Cache object, Cache object provides a rich API for the purpose of Redis services, the following is a specific use of examples:

````kotlin
fun redisDemo() {
    // Get the Redis Cache object named bbs
    var bbsCache: Cache? = Redis.use("bbs")
    bbsCache!!["key"] = "value"
    bbsCache.get<Any>("key")

    // Get Redis Cache object named news
    val newsCache = Redis.use("news")
    newsCache["k"] = "v"
    newsCache.get<Any>("k")

    //The first created Cache will become the main Cache, so you can save the cacheName parameter to get
    bbsCache = Redis.use()    // The main cache can save the cacheName parameter
    bbsCache!!["cloudopt"] = "awesome"
    }

````

````java
public void redisDemo() {
    // Get the Redis Cache object named bbs
    Cache bbsCache = Redis.use("bbs");
    bbsCache.set("key", "value");
    bbsCache.get("key");

    //Get Redis Cache object named news
    Cache newsCache = Redis.use("news");
    newsCache.set("k", "v");
    newsCache.get("k");

    // The first created Cache will become the main Cache, so you can save the cacheName parameter to get
    bbsCache = Redis.use();    // The main cache can save the cacheName parameter
    bbsCache.set("cloudopt", "awesome");
}
````
