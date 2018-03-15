## Jsoner

Jsoner是Cloudopt Next的Json工具类，几乎所有与Json有关的操作都是使用这个工具类的，默认使用[FastJson](https://github.com/alibaba/fastjson)。参数中没有指定反序列化的情况下将会返回底层json工具的对象，如FastJson是JSONObject。建议在使用Cloudopt Next期间所有Json有关的操作都使用这个帮助类。

````kotlin
fun help(){
    Jsoner.toJsonString(object)
    Jsoner.toJsonObject("json")
    Jsoner.toJsonObject("json",TestBean::class.java)
    Jsoner.toJsonArray("json")
    Jsoner.toJsonArray("json",TestBean::class.java)
}
````

````java
public void help(){
    Jsoner.INSTANCE.toJsonString(object);
    Jsoner.INSTANCE.toJsonObject("json");
    Jsoner.INSTANCE.toJsonObject("json",TestBean.class);
    Jsoner.INSTANCE.toJsonArray("json");
    Jsoner.INSTANCE.toJsonArray("json",TestBean.java);
}
````

## 自定义Jsoner

Jsoner是单例模式的，在初始化时会自动读取配置文件中的jsonProvider中的类名，如net.cloudopt.next.web.json.DefaultJSONProvider来进行初始化，如果您需要替换自己喜欢的Json支持库（如gson）可以创建一个新的JSONProvider并修改配置文件。

创建一个新的Provider非常简单，只需要实现JsonProvider类即可。您也可以参考默认的[DefaultJSONProvider](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-web/src/main/java/net/cloudopt/next/web/json/DefaultJSONProvider.kt)。

