﻿﻿﻿Cloudopt-next-logging is a handy logging plugin and one of the core components of cloudopt-next. Cloudopt-next-logging supports automatic switching of the JDK's own logs and slf4j. By default, cloudopt-next uses slf4j+logback. It is also recommended that you use the same logging framework.

Cloudopt-next-logging also supports automatic output of logs of different colors to the console based on the log level, which you can turn off manually. If you are using the cloudopt-next-web framework, configure it directly in the configuration file.

````kotlin
Colorer.enable = false
````

````java
Colorer.setEnable(false)
````

We recommend that you use cloudopt-next-logging as your logging tool during development to facilitate unified management. The use of cloudopt-next-logging is almost identical to that of slf4j and log4j.

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


