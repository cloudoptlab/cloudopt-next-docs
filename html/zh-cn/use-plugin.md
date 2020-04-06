## 使用插件

在Cloudopt Next使用插件非常简单，只需要在服务器启动前增加即可。

````kotlin
CloudoptServer.addPlugin(JooqPlugin())
CloudoptServer.run(App::class.java)
````

````java
CloudoptServer.addPlugin(new JooqPlugin());
CloudoptServer.run(App.class);
````

## 编写插件

编写一个自己的插件，只需要实现Plugin接口即可。如果在启动或者停止返回false，Cloudopt Next将会自动输出错误日志。

````kotlin
class TestPlugin:Plugin{

    override fun start(): Boolean {
        println("TestPlugin is starting!")
        return true
    }

    override fun stop(): Boolean {
        println("TestPlugin is stopping!")
        return true
    }

}
````

````java
public class TestPlugin implements Plugin {
    @Override
    public boolean start() {
        System.out.println("TestPlugin is starting!");
        return true;
    }

    @Override
    public boolean stop() {
        System.out.println("TestPlugin is starting!");
        return true;
    }
}
````

我们还提供了大量的工具来帮助你更方便的开发插件。

### 自动扫描注解

````kotlin
Classer.scanPackageByAnnotation(CloudoptServer.packageName, true, AutoKafka::class.java)
.forEach { clazz ->
    println(clazz)
    }
}
````

### 自动创建对象

````kotlin
var obj = Beaner.newInstance<KafkaListener>(clazz)
````

### 读取配置文件

````kotlin
var config = ConfigManager.init("test")
````

### 获取所有的路由器

````kotlin
var controllers = CloudoptServer.controllers
````