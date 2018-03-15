## 使用Render

Render是Resource类中已经写好的语法糖，当您需要输出东西时直接调用方法即可。目前支持的视图有Html、Json、Text、FreeMaker、Hbs、Beetl。这几种都是可以在Resource中直接使用的。

需要注意的是FreeMaker、Hbs、Beetl都需要自行引用相应的依赖，Cloudopt Next并没有附带。更多代码案例可以看[GitHub](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-web/src/test/java/net/cloudopt/next/web/test/controller/IndexController.kt)。

渲染页面时Render会根据配置文件中的webroot项的配置，自动读取文件，默认是在templates文件夹下。


## 创建自己的Render

如果您需要使用Cloudopt Next尚未支持的模板引擎，您可以自行编写一个Render。建议参考[JsonRender](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-web/src/main/java/net/cloudopt/next/web/render/JsonRender.kt)。

创建好Java类后，在服务器启动前添加进去。

````kotlin
CloudoptServer.addRender("custom",JsonRender())
````

````java
CloudoptServer.addRender("custom",new JsonRender());
````

使用时只需要在路由中加上名字调用即可。

````kotlin
render("custom","text")
````

````java
render("custom","text");
````

## 修改默认的Render

默认情况下，如果直接调用render方法，会自动调用JsonRender。如果您需要修改默认的Render，需要调用RenderFactory进行修改。

````kotlin
RenderFactory.setDefaultRender("json")
````

````java
RenderFactory.INSTANCE.setDefaultRender("json");
````

## 静态资源

CSS、JS、图片等静态资源文件是要与模板文件分开的，默认放在static文件夹下，当页面需要引用静态文件时直接引用static文件夹即可。

````html
<link rel="shortcut icon" href="/static/favicon.ico" type="image/x-icon"/>
````