cloudopt-plugin-client 是对 http 客户端的一个简易封装，基于 vertx 体系，可以简单实现异步请求服务器的过程。

在使用前请先自行引用相应的依赖，请自行添加版本号。

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-client</artifactId>
</dependency>
````

````kotlin
var client = HttpClient("https://www.cloudopt.net")

client.addParam("key","value")
    
client.addHeader("key","value")

client.get("/testUrl").send { result ->
    println(Jsoner.toJsonString(result.result().bodyAsString()))
}
````

如果是 post 、 put 等请求，直接将上面示例中 get 方法名进行更换即可。如果需要发送表单数据，将 send 方法换成 sendForm；如果需要发送 json 数据将 send 方法换成 sendJson，以此类推。