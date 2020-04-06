## Create a configuration file

The Cloudopt Next configuration file uses the Json format. Let us look at a simple example. Cloudopt Next will automatically find if the application.json file exists in the project and will automatically read it if it exists.

````json
{
  "packageName": "net.cloudopt.next.example",
  "cookieCors": true,
  "port": 9090
}
````

| Name     | Default| Description|
|:--------:|:---------:|:-------|
| env| null|After filling in, the configuration file of application-${env}.json will be read automatically, and the configuration in application. JSON will be overwritten.        |
| banner| true| Whether to display Banner at startup.      |
| bannerName| "banner.txt"| Banner file name.      |
| devbug| true| Whether to is developer mode.      |
| showRoute| true| Whether to display routing information during access.      |
| cors| true| Whether to open CORS, enabling CORS will allow API calls across domains.      |
| packageName| ""| The name of the package where the project is located.      |
| port| 8080| Listening port.      |
| staticPackage| "static"| The name of the folder where the static resource file is located.      |
| templates| "templates"| The name of the folder where the template file is located.      |
| errorHandler| "net.cloudopt.next.web.handler.DefaultErrorHandler"| Error interceptor package name and class name.      |
| jsonProvider| "net.cloudopt.next.json.DefaultJSONProvider"| The package name and class name of the Json implementation class.      |
| indexPage| "index.html"| The home page file name of the static resource folder.      |
| cookieCors| true| Whether to allow cookies to be passed at the same time under cross-domain call API conditions.      |
| bodyLimit| 50L * 1024 * 1024| File upload size limit, in units of b.      |
| logColor| true| Whether to use color log output.      |
| timeout| 2L * 60 * 1000| HTTP request timeout in ms.      |

## Get configuration

When the server starts up, it reads the configuration file and converts it to an object for management by ConfigManager. If you need to modify the configuration or obtain the configuration, you can directly purchase or alter it through the ConfigManager.

````kotlin
ConfigManager.webConfig.devbug = true
println(ConfigManager.webConfig.devbug)
````

````java
ConfigManager.getWebConfig().setDevbug(true);
System.out.println(ConfigManager.getWebConfig().getDevbug());
​`````

## Get custom configuration

If you need to get the custom configuration in application.yml, you can directly get the configuration under net.cloudopt.next.test by ConfigManager.init("test") or ConfigManager.initObject("test",TestBean.class).Ideal for plug-in development.
````

## Advanced configuration

Cloudopt next supports setting vertx, vertxhttpserver, and vertxdeployment settings directly in application.json. If you are very familiar with the vertx system, you can directly modify the settings in application.json to configure vertx.