## 通过main方法运行

Cloudopt Next是通过main方法启动服务器并运行的，这是一个标准的方法，它遵循Java对于一个应用程序入口点的约定。在服务器启动后Cloudopt Next将会自动监听设置好的端口（默认是8080）。通过run方法获取到项目的路径后，Cloudopt Next会自动扫描项目中所有的文件并自动注册。代码如下：

````kotlin
fun main(args: Array<String>) {
    CloudoptServer.run(App::class)
}
````

````java
public static void main(String[] args){
    CloudoptServer.run(App.class);
}
````

run方法中您可以填入启动类的类名、包名，如果什么都不填的话将会自动读取配置文件来获取包名。

## 通过包名启动

````kotlin
fun main(args: Array<String>) {
    CloudoptServer.run("net.cloudopt.next.example")
}
````

````java
public static void main(String[] args){
    CloudoptServer.run("net.cloudopt.next.example");
}
````

## 通过配置文件启动

> 如果您希望省略参数的话，请务必在配置文件中配置好包名，具体可参考[配置文件](/zh-cn/config.md)。

````kotlin
fun main(args: Array<String>) {
    CloudoptServer.run()
}
````

````java
public static void main(String[] args){
    CloudoptServer.run();
}
````

## 控制台输出

如果您启动成功的话会看到类似下面的控制台输出：
````shell
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - [PLUGIN] Registered plugin：net.cloudopt.next.jooq.JooqPlugin
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] -  ______  __      ______  __  __  _____   ______  ______  ______
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - /\  ___\/\ \    /\  __ \/\ \/\ \/\  __-./\  __ \/\  == \/\__  _\
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - \ \ \___\ \ \___\ \ \/\ \ \ \_\ \ \ \/\ \ \ \/\ \ \  _-/\/_/\ \/
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] -  \ \_____\ \_____\ \_____\ \_____\ \____-\ \_____\ \_\     \ \_\
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] -   \/_____/\/_____/\/_____/\/_____/\/____/ \/_____/\/_/      \/_/
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - 
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - Java Version: 1.8.0_131
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - Java Provider: Oracle Corporation
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - System: Windows 10
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - Time: 2018-03-04 18:39:12
-------------------------------------------------------------------------------------------
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - [FAILURE HANDLER] Registered failure handler：net.cloudopt.next.web.handler.DefaultErrorHandler
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - [HANDLER] Registered handler：net.cloudopt.next.web.handler.WafHandler
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - [HANDLER] Registered handler：net.cloudopt.next.web.handler.CorsHandler
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - [HANDLER] Registered handler：net.cloudopt.next.web.handler.ShowRouteHandler
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - [HANDLER] Registered handler：net.cloudopt.next.web.handler.CookieCorsHandler
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - [RESOURCE] Registered Resource :get | /
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - [RESOURCE] Registered Resource :get | /api/v1/todo
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - [RESOURCE] Registered Resource :put | /api/v1/todo/:id
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - [RESOURCE] Registered Resource :delete | /api/v1/todo/:id
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - [RESOURCE] Registered Resource :post | /api/v1/todo
==========================================================================================================
[Cloudopt Next] 2018-03-04 18:39:12 net.cloudopt.next.web.CloudoptServer [INFO ] - Cloudopt Next started is success!
==========================================================================================================
````

控制台输出包含两个部分，第一个部分是Banner，第二个部分是会输出注册成功的路由、Handler等等。如果您需要替换Banner，只需要在项目的resource文件夹下新建一个banner.txt即可。为了帮助您更好的输出Banner，Cloudopt Next支持自动替换Banner中的变量，目前Cloudopt Next支持以下变量：

````shell
Java Version: ${java.version}
Java Provider: ${java.vendor}
System: ${os}
Time: ${time}
````

## 完整例子

为了方便您的学习和使用，我们提供了一个简单的Example，您可以通过访问[GitHub](https://github.com/cloudoptlab/cloudopt-next-example)获取。