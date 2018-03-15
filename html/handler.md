Handler is a global interceptor. Let's take a look at the ShowRouteHandler that comes with Cloudopt Next.

````kotlin
@AutoHandler
class ShowRouteHandler : Handler() {

    override fun handle() {
        if (ConfigManager.webConfig.showRoute) {
            val df = SimpleDateFormat("yyyy-MM-dd HH:mm:ss")
            logger.info("Match route ----------------- " + df.format(Date())
                    + " ------------------------------")
            logger.info("Method       : " + request?.method())
            logger.info("Path         : " + request?.uri())
            logger.info("User-Agent   : " + request?.getHeader("User-Agent"))
            logger.info("Params       : " + Jsoner.toJsonString(request?.params()?.entries() ?: listOf<Map.Entry<String, String>>()))
            logger.info("Cookie       : " + Jsoner.toJsonString(request.getHeader("Cookie") ?: ""))
            logger.info(
                    "--------------------------------------------------------------------------------")
        }
    }

    companion object {
        private val logger = Logger.getLogger(ShowRouteHandler::class.java)
    }
}
````

If you need to create your own Handler, you just need to extend the Handler class. If the @AutoHandler annotation is added to the class, Cloudopt Next will automatically register it at startup. If you only want to manually register, you can manually increase before the server starts.

````kotlin
CloudoptServer.addHandler(ShowRouteHandler())
CloudoptServer.run(App::class.java)
````

````java
CloudoptServer.addHandler(new ShowRouteHandler());
CloudoptServer.run(App.class);
````
