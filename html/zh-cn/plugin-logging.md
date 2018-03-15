cloudopt-next-logging是一个非常好用的日志插件，同时也是cloudopt-next的核心组件之一。cloudopt-next-logging支持自动切换JDK自身的日志和slf4j，默认情况下cloudopt-next使用的是slf4j+logback，也建议您使用同样的日志框架。

cloudopt-next-logging还支持自动根据日志的级别向控制台输出不同颜色的日志，您可以手动将其关闭。如果您正在使用cloudopt-next-web框架，则直接在配置文件中配置即可。

````kotlin
Colorer.enable = false
````

````java
Colorer.setEnable(false)
````

我们建议您在开发过程中使用cloudopt-next-logging作为您的日志工具，方便统一管理。cloudopt-next-logging的使用方法与slf4j和log4j等几乎是一模一样。

````kotlin
private val logger = Logger.getLogger(TestCase::class.java)
logger.debug("debug")
logger.info("info")
logger.warn("warn")
logger.error("error")
````

````java
private static Logger logger = Logger.getLogger(TestCase.class);
logger.debug("debug");
logger.info("info");
logger.warn("warn");
logger.error("error");
````