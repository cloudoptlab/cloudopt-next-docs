## Create a configuration file

The Cloudopt Next configuration file uses the Yaml format. Let us look at a simple example. Cloudopt Next will automatically find if the application.yml file exists in the project and will automatically read it if it exists.

````yaml
net:
  cloudopt:
    next:
      web:
        packageName: "net.cloudopt.next.example"
        cookieCors: "true"
````

The cloudopt-next-web project reads under net.cloudopt.next.web, and net.cloudopt.next.web will be omitted from the table.

| Name     | Default| Description|
|:--------:|:---------:|:-------|
| banner| true| Whether to display Banner at startup.      |
| bannerName| "banner.txt"| Banner file name.      |
| dev| true| Whether to is developer mode.      |
| showRoute| true| Whether to display routing information during access.      |
| cors| true| Whether to open CORS, enabling CORS will allow API calls across domains.      |
| packageName| ""| The name of the package where the project is located.      |
| port| 8080| Listening port.      |
| static| "static"| The name of the folder where the static resource file is located.      |
| webroot| "templates"| The name of the folder where the template file is located.      |
| errorHandler| "net.cloudopt.next.web.handler.DefaultErrorHandler"| Error interceptor package name and class name.      |
| jsonProvider| "net.cloudopt.next.web.json.DefaultJSONProvider"| The package name and class name of the Json implementation class.      |
| indexPage| "index.html"| The home page file name of the static resource folder.      |
| cookieCors| true| Whether to allow cookies to be passed at the same time under cross-domain call API conditions.      |
| bodyLimit| 50L * 1024 * 1024| File upload size limit, in units of b.      |
| logColor| true| Whether to use color log output.      |
| timeout| 2L * 60 * 1000| HTTP request timeout in ms.      |

## Developer mode

When dev is true, the application-dev.yml file is reread and the application.yml setting is overwritten. And vice versa, read application-pro.yml when dev is false. Help you separate development environment and production environment.

## Get configuration

When the server starts up, it reads the configuration file and converts it to an object for management by ConfigManager. If you need to modify the configuration or obtain the configuration, you can directly purchase or alter it through the ConfigManager.

````kotlin
ConfigManager.webConfig.dev = true
println(ConfigManager.webConfig.dev)
````

````java
ConfigManager.getWebConfig().setDev(true);
System.out.println(ConfigManager.getWebConfig().getDev());
​`````

## Get custom configuration

If you need to get the custom configuration in application.yml, you can directly get the configuration under net.cloudopt.next.test by ConfigManager.initMap("test") or ConfigManager.initMap("test",TestBean.class).Ideal for plug-in development.
````