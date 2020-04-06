## Use plug-ins

Using plug-ins with Cloudopt Next is very simple and only needs to be added before the server starts.

````kotlin
CloudoptServer.addPlugin(JooqPlugin())
CloudoptServer.run(App::class.java)
````

````java
CloudoptServer.addPlugin(new JooqPlugin());
CloudoptServer.run(App.class);
````

## Write a plugin

To write your own plugin, you only need to implement the Plugin interface. If you start or stop returning false, Cloudopt Next will automatically output an error log.

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
### Auto scan annotation

````kotlin
Classer.scanPackageByAnnotation(CloudoptServer.packageName, true, AutoKafka::class.java)
.forEach { clazz ->
    println(clazz)
    }
}
````

### Auto creat object

````kotlin
var obj = Beaner.newInstance<KafkaListener>(clazz)
````

### Auto read config

````kotlin
var config = ConfigManager.init("test")
````

### Auto get all of controllers

````kotlin
var controllers = CloudoptServer.controllers
````