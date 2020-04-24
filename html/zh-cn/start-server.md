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
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO:  ______  __      ______  __  __  _____   ______  ______  ______
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: /\  ___\/\ \    /\  __ \/\ \/\ \/\  __-./\  __ \/\  == \/\__  _\
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: \ \ \___\ \ \___\ \ \/\ \ \ \_\ \ \ \/\ \ \ \/\ \ \  _-/\/_/\ \/
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO:  \ \_____\ \_____\ \_____\ \_____\ \____-\ \_____\ \_\     \ \_\
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO:   \/_____/\/_____/\/_____/\/_____/\/____/ \/_____/\/_/      \/_/
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: 
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: Java Version: 1.8.0_242
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: Java Provider: Eclipse OpenJ9
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: System: Mac OS X
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: Time: 2020-04-06 21:01:19
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: Listener Port: 9090
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: -------------------------------------------------------------------------------------------
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: [FAILURE HANDLER] Registered failure handler：net.cloudopt.next.web.handler.DefaultErrorHandler
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: [HANDLER] Registered handler：net.cloudopt.next.web.handler.ShowRouteHandler
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: [HANDLER] Registered handler：net.cloudopt.next.web.handler.CorsHandler
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: [HANDLER] Registered handler：net.cloudopt.next.web.handler.CookieCorsHandler
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: [HANDLER] Registered handler：net.cloudopt.next.web.handler.WafHandler
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: ==========================================================================================================
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: 🐋 Cloudopt Next started is success!
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: http://127.0.0.1:8080
[Cloudopt Next] 2020-04-06 21:01:19 net.cloudopt.next.web.CloudoptServer [INFO ] - ℹ️ INFO: ==========================================================================================================
````

控制台输出包含两个部分，第一个部分是Banner，第二个部分是会输出注册成功的路由、Handler等等。如果您需要替换Banner，只需要在项目的resource文件夹下新建一个banner.txt即可。为了帮助您更好的输出Banner，Cloudopt Next支持自动替换Banner中的变量，目前Cloudopt Next支持以下变量：

````shell
Java Version: ${java.version}
Java Provider: ${java.vendor}
System: ${os}
Time: ${time}
````

## 热部署

Cloudopt Next 内置了热部署，在使用前你需要先开启 IDE 的热部署相关设置。在运行设置中将 Main Class 设置为 `net.cloudopt.next.web.CloudoptLauncher` ，Program arguments 设置为放置了 `CloudoptServer.run()` 的类即可。默认会监测项目中的 class 文件发生变动时会自动重启 CloudoptServer。

> 如果你是用 Kotlin 的话可能会出现重启较慢的问题，可以考虑设置成增量更新，或者是手动编译修改的文件。

## 完整例子

为了方便您的学习和使用，我们提供了一个简单的Example，您可以通过访问[GitHub](https://github.com/cloudoptlab/cloudopt-next-example)获取。