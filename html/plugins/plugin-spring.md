﻿If you need to support spring in cloudopt-next-web, you only need to configure the cloudopt-next-web configuration file and add the plugin before the server starts. Need to use spring management XML separated by commas.

Please refer to the appropriate dependencies before use, please add the version number yourself.

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-spring</artifactId>
</dependency>
````

````json
{
  "spring": {
    "xml": "classpath:applicationContext.xml,classpath:applicationContext2.xml"
  }
}
````

````kotlin
fun main(args: Array<String>) {
    CloudoptServer.addPlugin(SpringPlugin())
    CloudoptServer.run(TestCase::class)
}
````

````java
fun main(args: Array<String>) {
    CloudoptServer.addPlugin(SpringPlugin());
    CloudoptServer.run(TestCase.class);
}
````

