## 创建配置文件

Cloudopt Next的配置文件使用的是Yaml格式的。让我们看一个简单的例子。Cloudopt Next会自动查找项目中是否存在application.yml文件，如果存在则会自动读取。

````yaml
net:
  cloudopt:
    next:
      web:
        packageName: "net.cloudopt.next.example"
        cookieCors: "true"
````

cloudopt-next-web项目读取的都是在net.cloudopt.next.web下的，表格中将省略net.cloudopt.next.web。

| Name     | Default| Description|
|:--------:|:---------:|:-------|
| banner| true| 是否在启动时显示Banner。      |
| bannerName| "banner.txt"| Banner文件的文件名。      |
| dev| true| 是否是开发者模式。      |
| showRoute| true| 是否在访问时显示路由信息。      |
| cors| true| 是否打开CORS，开启后允许跨域调用API。      |
| packageName| ""| 项目所在包名。      |
| port| 8080| 监听端口。      |
| static| "static"| 静态资源文件所在文件夹名。      |
| webroot| "templates"| 模板文件所在文件夹名。      |
| errorHandler| "net.cloudopt.next.web.handler.DefaultErrorHandler"| 错误拦截器的包名和类名。      |
| jsonProvider| "net.cloudopt.next.web.json.DefaultJSONProvider"| Json实现类的包名及类名。      |
| indexPage| "index.html"| 静态资源文件夹的主页文件名。      |
| cookieCors| true| 是否允许在跨域调用API情况的下同时传递Cookie。      |
| bodyLimit| 50L * 1024 * 1024| 文件上传大小限制，单位为b。      |
| logColor| true| 是否使用彩色的日志输出。      |
| timeout| 2L * 60 * 1000| HTTP请求超时时间，单位为ms。      |

## 开发模式

当dev为true时会再次读取application-dev.yml文件，并覆盖application.yml的设置。反之亦然，当dev为false时读取application-pro.yml。帮助您分开开发环境和生产环境。

## 获取配置

服务器启动时会读取配置文件并转为对象交给ConfigManager进行管理。您如果需要修改配置或者获取配置可以直接通过ConfigManager进行获取或修改。

````kotlin
ConfigManager.webConfig.dev = true
println(ConfigManager.webConfig.dev)
````

````java
ConfigManager.getWebConfig().setDev(true);
System.out.println(ConfigManager.getWebConfig().getDev());
`````

## 获取自定义的配置

如果您需要获取application.yml中的自定义的配置，可以直接通过ConfigManager.initMap("test")或者ConfigManager.initMap("test",TestBean.class)，会自动获取net.cloudopt.next.test下的配置，非常适合用于插件开发。