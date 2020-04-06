SockJS是一个客户端JavaScript库和协议，它提供了一个简单的类似WebSocket的接口，允许您连接到SockJS服务器，而不管实际的浏览器或网络是否允许真正的WebSockets。

它通过支持浏览器和服务器之间的各种不同传输，并根据浏览器和网络功能在运行时选择一种传输来实现这一点。

所有这些对你来说都是透明的——你只需要看到一个类似WebSocket的界面，它就可以工作了。

有关SockJS的更多信息，请参见[SockJS网站]（https://github.com/SockJS/SockJS-client）。

Cloudopt Next 中内置了对 SockJS 的支持，你只需要声明一个注解即可（注意路由的最后一个字符必须为`/*`）。

````kotlin
@SocketJS("/socket/api/*")
class SocketController : SocketJSResource {
    override fun handler(socket: SockJSSocket) {
        println(socket)
        socket.handler {message ->
            println(message)
            socket.write("Hello world!")
        }
    }
}
````

`message` 就是用户传递过来的消息，你可以通过 `socket.write()` 方法给用户发消息。如果你希望做一个聊天应用的话，建议你保存 socket 对象，每个用户在重新连接前应该是对应一个唯一的 socket 对象。