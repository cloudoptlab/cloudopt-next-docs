如果您需要在cloudopt-next-web中支持spring的话，您只需要配置好cloudopt-next-web的配置文件然后在服务器启动前增加插件即可。需要用spring管理的xml用英文逗号分开。

在使用前请先自行引用相应的依赖，请自行添加版本号。

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