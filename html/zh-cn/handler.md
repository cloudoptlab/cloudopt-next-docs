Handler是一个全局的拦截器，我们来看看Cloudopt Next自带的ShowRouteHandler。

````kotlin
@AutoHandler
class ShowRouteHandler : Handler() {

    override fun preHandle(resource: Resource) {
        //在请求处理之前进行调用
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
        //请求处理之后进行调用，但是在视图被渲染之前
    }

    override fun afterCompletion(resource: Resource) {
        //在整个请求结束之后被调用
    }

    companion object {
        private val logger = Logger.getLogger(ShowRouteHandler::class.java)
    }
}
````

如果您需要创建一个自己的Handler，只需要继承Handler类即可。如果类上面添加了@AutoHandler注解，Cloudopt Next在启动时会自动注册。如果您只想手动注册的话，可以在服务器启动前手动增加。

````kotlin
CloudoptServer.addHandler(ShowRouteHandler())
CloudoptServer.run(App::class.java)
````

````java
CloudoptServer.addHandler(new ShowRouteHandler());
CloudoptServer.run(App.class);
````
