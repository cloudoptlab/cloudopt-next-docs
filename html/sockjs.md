SockJS is a client side JavaScript library and protocol which provides a simple WebSocket-like interface allowing you to make connections to SockJS servers irrespective of whether the actual browser or network will allow real WebSockets.

It does this by supporting various different transports between browser and server, and choosing one at run-time according to browser and network capabilities.

All this is transparent to you - you are simply presented with the WebSocket-like interface which just works.

Please see the [SockJS website](https://github.com/sockjs/sockjs-client) for more information on SockJS.

Cloudopt next has built-in support for sockjs. You only need to declare one annotation (note that the last character of the route must be '/ *').

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

`message` is the message delivered by the user. You can send a message to the user through the `socket.write()` method. If you want to make a chat application, it is recommended that you save the socket object. Each user should be a unique socket object before reconnecting.