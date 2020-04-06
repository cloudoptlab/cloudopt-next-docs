cloudopt-next-redis，是移植于 JFinal 的RedisPlugin，使用 RedisPlugin 可以极度方便的使用redis，该插件不仅提供了丰富的API，而且还同时支持多 redis 服务端。Redis 拥有超高的性能，丰富的数据结构，天然支持数据持久化，是目前应用非常广泛的 nosql 数据库。对于 redis 的有效应用可极大提升系统性能，节省硬件成本。

在使用前请先自行引用相应的依赖。请自行添加版本号。

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-redis</artifactId>
</dependency>
````

## 配置

cloudopt-next-redis同样支持自动读取配置文件。

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

所有参数都不是必须填写的，默认的 host 为 localhost，端口为 6379。

## 启动

在配置完成后您需要在服务器启动前启动插件。

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

Redis与Cache联合起来可以非常方便地使用Redis服务，Redis对象通过use()方法来获取到Cache对象，Cache对象提供了丰富的API用于使用Redis服务，下面是具体使用示例：

````kotlin
fun redisDemo() {
    // 获取名称为bbs的Redis Cache对象
    var bbsCache: Cache? = Redis.use("bbs")
    bbsCache!!["key"] = "value"
    bbsCache.get<Any>("key")

    // 获取名称为news的Redis Cache对象
    val newsCache = Redis.use("news")
    newsCache["k"] = "v"
    newsCache.get<Any>("k")

    // 最先创建的Cache将成为主Cache，所以可以省去cacheName参数来获取
    bbsCache = Redis.use()    // 主缓存可以省去cacheName参数
    bbsCache!!["cloudopt"] = "awesome"
    }

````

````java
public void redisDemo() {
    // 获取名称为bbs的Redis Cache对象
    Cache bbsCache = Redis.use("bbs");
    bbsCache.set("key", "value");
    bbsCache.get("key");

    // 获取名称为news的Redis Cache对象
    Cache newsCache = Redis.use("news");
    newsCache.set("k", "v");
    newsCache.get("k");

    // 最先创建的Cache将成为主Cache，所以可以省去cacheName参数来获取
    bbsCache = Redis.use();    // 主缓存可以省去cacheName参数
    bbsCache.set("cloudopt", "awesome");
}
````