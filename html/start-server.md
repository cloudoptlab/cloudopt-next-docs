##Run through the main method

Cloudopt Next starts the server and runs it through the main method. It is a standard method. It follows Java's convention for an application entry point. Cloudopt Next will automatically monitor the set port (default is 8080) after the server starts. After getting the path to the project through the run method, Cloudopt Next automatically scans all the files in the project and automatically registers it. Code show as below:

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

In the run method, you can fill in the class name and package name of the startup class. If nothing is filled, the configuration file will be automatically read to obtain the package name.

## Start with the package name

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

## Start through configuration file

> If you wish to omit the parameters, be sure to configure the package name in the configuration file. For details, refer to [Configuration File](/config.md).

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

## Console output

If you start successfully you will see console output similar to the following:
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

he console output contains two parts, the first part is the Banner, and the second part is to output the successfully registered route, Handler, and so on. If you need to replace Banner, just create a new banner.txt under the project's resource folder. To help you better export Banner, Cloudopt Next supports automatic replacement of variables in Banner. Currently Cloudopt Next supports the following variables:

````shell
Java Version: ${java.version}
Java Provider: ${java.vendor}
System: ${os}
Time: ${time}
````

##Complete example

To facilitate your learning and use, we provide a simple Example that you can obtain by visiting [GitHub] (https://github.com/cloudoptlab/cloudopt-next-example).

`