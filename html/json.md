## Jsoner

Jsoner is Cloudopt Next's Json utility class. Almost all Json-related operations use this utility class. By default, [FastJson](https://github.com/alibaba/fastjson) is used. If deserialization is not specified in the argument, the underlying Json tool object will be returned. For example, FastJson is a JSONObject. It is recommended that all Json-related operations use this helper class when using Cloudopt Next.

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

## Custom Jsoner

Jsoner is a singleton mode. It will automatically read the class name in the jsonProvider in the configuration file, such as net.cloudopt.next.web.json.DefaultJSONProvider to initialize, if you need to replace your favorite Json support library. (e.g. gson) You can create a new JSONProvider and modify the configuration file.

Creating a new Provider is very simple, just implement the JsonProvider class. You can also refer to the default [DefaultJSONProvider](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-web/src/main/java/net/cloudopt/next/web/json / DefaultJSONProvider.kt).

