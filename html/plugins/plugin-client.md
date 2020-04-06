cloudopt-next-plugin is a simple encapsulation of HTTP client. Based on vertx system, it can simply implement the process of asynchronous request server.

Before using, please refer to the corresponding dependency by yourself, and add the version number by yourself.

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

If it is a post, put or other request, you can directly change the get method name in the above example. If you need to send form data, change the send method to sendform; if you need to send JSON data, change the send method to sendjson, and so on.