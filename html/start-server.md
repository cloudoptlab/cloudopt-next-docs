﻿##Run through the main method

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