## Jsoner

Jsoner 是 Cloudopt Next 的 Json 工具类，几乎所有与 Json 有关的操作都是使用这个工具类的，默认使用[FastJson](https://github.com/alibaba/fastjson)。参数中没有指定反序列化的情况下将会返回底层json工具的对象，如 FastJson 是 JSONObject。建议在使用 Cloudopt Next 期间所有 Json 有关的操作都使用这个帮助类。

````kotlin
fun help(){
    Jsoner.toJsonString(object)
    Jsoner.toJsonMap("json")
    Jsoner.toJsonObject("json",TestBean::class.java)
    Jsoner.toJsonArray("json",TestBean::class.java)
    Jsoner.read("testfile.json")
}
````

````java
public void help(){
    Jsoner.toJsonString(object);
    Jsoner.toJsonMap("json");
    Jsoner.toJsonObject("json",TestBean.class);
    Jsoner.toJsonArray("json",TestBean.java);
    Jsoner.read("testfile.json");
}
````

## 自定义Jsoner

Jsoner是单例模式的，在初始化时会自动读取配置文件中的 jsonProvider 中的类名，如net.cloudopt.next.json.DefaultJSONProvider 来进行初始化，如果您需要替换自己喜欢的 Json 支持库（如gson）可以创建一个新的 JSONProvider 并修改配置文件。

创建一个新的 Provider 非常简单，只需要实现 JsonProvider 类即可。您也可以参考默认的[DefaultJSONProvider](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-web/src/main/java/net/cloudopt/next/web/json/DefaultJSONProvider.kt)。

