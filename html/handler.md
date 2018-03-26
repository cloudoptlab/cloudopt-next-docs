Handler is a global interceptor. Let's take a look at the ShowRouteHandler that comes with Cloudopt Next.

````kotlin
@AutoHandler
class ShowRouteHandler : Handler() {

    override fun preHandle(resource: Resource) {
        //The call is made before the request is processed.
        if (ConfigManager.webConfig.showRoute) {
            val df = SimpleDateFormat("yyyy-MM-dd HH:mm:ss")
            logger.info("Match route ----------------- " + df.format(Date())
                    + " ------------------------------")
            logger.info("Method       : " + resource.request.method())
            logger.info("Path         : " + resource.request.uri())
            logger.info("User-Agent   : " + resource.request.getHeader("User-Agent"))
            logger.info("Params       : " + Jsoner.toJsonString(resource.request.params()?.entries() ?: "[]"))
            logger.info("Cookie       : " + Jsoner.toJsonString(resource.request.getHeader("Cookie") ?: ""))
            logger.info(
                    "--------------------------------------------------------------------------------")
        }
    }

    override fun postHandle(resource: Resource) {
        //The call is made after the request is processed, but before the view is rendered.
    }

    override fun afterCompletion(resource: Resource) {
        //Invoked after the entire request is complete.
    }

    companion object {
        private val logger = Logger.getLogger(ShowRouteHandler::class.java)
    }
}
````

If you need to create your Handler, you just need to extend the Handler class. If the @AutoHandler annotation is added to the level, Cloudopt Next will automatically register it at startup. If you only want to record manually, you can manually increase before the server starts.

````kotlin
CloudoptServer.addHandler(ShowRouteHandler())
CloudoptServer.run(App::class.java)
````

````java
CloudoptServer.addHandler(new ShowRouteHandler());
CloudoptServer.run(App.class);
````
