## 创建配置文件

Cloudopt Next 的配置文件使用的是 json 格式的。让我们看一个简单的例子。Cloudopt Next 会自动查找项目中是否存在 application.json 文件，如果存在则会自动读取。

````json
{
  "packageName": "net.cloudopt.next.example",
  "cookieCors": true,
  "port": 9090
}
````

| Name     | Default| Description|
|:--------:|:---------:|:-------|
| env| null| 填写后会自动读取 application-${env}.json 的配置文件，并覆盖 application.json 中的配置。       |
| banner| true| 是否在启动时显示Banner。      |
| bannerName| "banner.txt"| Banner文件的文件名。      |
| devbug| true| 是否是开发者模式。      |
| showRoute| true| 是否在访问时显示路由信息。      |
| cors| true| 是否打开CORS，开启后允许跨域调用API。      |
| packageName| ""| 项目所在包名。      |
| port| 8080| 监听端口。      |
| staticPackage| "static"| 静态资源文件所在文件夹名。      |
| templates| "templates"| 模板文件所在文件夹名。      |
| errorHandler| "net.cloudopt.next.web.handler.DefaultErrorHandler"| 错误拦截器的包名和类名。      |
| jsonProvider| "net.cloudopt.next.json.DefaultJSONProvider"| Json实现类的包名及类名。      |
| indexPage| "index.html"| 静态资源文件夹的主页文件名。      |
| cookieCors| true| 是否允许在跨域调用API情况的下同时传递Cookie。      |
| bodyLimit| 50L * 1024 * 1024| 文件上传大小限制，单位为b。      |
| logColor| true| 是否使用彩色的日志输出。      |
| timeout| 2L * 60 * 1000| HTTP请求超时时间，单位为ms。      |

## 获取配置

服务器启动时会读取配置文件并转为对象交给 ConfigManager 进行管理。您如果需要修改配置或者获取配置可以直接通过 ConfigManager 进行获取或修改。

````kotlin
ConfigManager.webConfig.devbug = true
println(ConfigManager.webConfig.devbug)
````

````java
ConfigManager.getWebConfig().setDevbug(true);
System.out.println(ConfigManager.getWebConfig().getDevbug());
`````

## 获取自定义的配置

如果您需要获取 application.yml 中的自定义的配置，可以直接通过 ConfigManager.init("test") 或者 ConfigManager.initObject("test",TestBean.class)，会自动获取 test 下的配置，非常适合用于插件开发。


## 高级配置

cloudopt-next 支持直接在 application.json 中设置 vertx、vertxHttpServer、vertxDeployment 相关的设置，如果你对 vertx 体系非常熟悉的话，可以直接通过在 application.json 修改设置来达到配置 vertx 的目的。