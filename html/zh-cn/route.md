## 使用注解

Cloudopt Next中的路由是通过注解来使用的，任意类继承Resource类并在头部增加@API即可。如：

````kotlin
@API("/")
class IndexController : Resource() {

    @GET
    fun get(){
        renderText("Hello World!")
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET
    public void get(){
        renderText("Hello World!");
    }

}
````

## @API

Cloudopt Next在启动时会自动扫描含有@API注解的类，并自动解析这个类里面的所有的方法。具体原理可以参照[深入路由原理](/zh-cn/deep-route.md)一章。

@API中可以设置具体的URL，这个类中的方法也将自动继承。

如：

@API("/")  =>  http://localhost:8080/

@API("/test")  =>  http://localhost:8080/test

## RESTful

Cloudopt Next支持@GET、@POST、@PUT、@DELETE、@PATCH五种注解，分别对应HTTP请求中的五种method。RESTful相关的注解只能使用在方法上，与@API一样是支持配置URL的。Cloudopt Next会将@API中配置的URL与RESTful注解中配置的URL自动拼接到一起。

如：

````kotlin
@API("/")
class IndexController : Resource() {

    @GET("hello")
    fun get(){
        renderText("Hello World!")
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET("hello")
    public void get(){
        renderText("Hello World!");
    }

}
````

您将需要通过 GET http://localhost:8080/hello 进行访问。

## 获取参数

如果您需要获取客户端传递过来的参数，您可以直接在方法中使用getParam()方法获取。

````kotlin
@API("/")
class IndexController : Resource() {

    @GET
    fun get(){
        renderText(getParam("name") ?: "")
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET
    public void get(){
        renderText(getParam("name"));
    }

}
````

## 获取URL参数

如果您需要获取URL上的参数，需要在RESTful注解中设置:参数名。

````kotlin
@API("/")
class IndexController : Resource() {

    @GET("/:name")
    fun get(){
        renderText(getParam("name") ?: "")
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET("/:name")
    public void get(){
        renderText(getParam("name"));
    }

}
````


## 获取表单数据

如果您需要获取客户端传递过来的参数，您可以直接在方法中使用getParam()方法获取。

````kotlin
@API("/")
class IndexController : Resource() {

    @GET
    fun get(){
        renderText(getParam("name") ?: "")
        renderJson(getParam(TestBean::class.java))
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET
    public void get(){
        renderText(getAttr("name"));
        renderJson(getAttr(TestBean::class.java));
    }

}
````

## Cookie

Cookie还支持更多设置，具体可以看setCookie方法的参数注释。

````kotlin
@API("/")
class IndexController : Resource() {

    @GET
    fun get(){
        setCookie("key","value")
        getCookie("key")
        delCookie("key")
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET
    public void get(){
        setCookie("key","value");
        getCookie("key");
        delCookie("key");
    }

}
````


## HTTP Header

````kotlin
@API("/")
class IndexController : Resource() {

    @GET
    fun get(){
        setHeader("key","value")
        getHeader("key")
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET
    public void get(){
        setHeader("key","value");
        getHeader("key");
    }

}
````

## 获取IP

````kotlin
@API("/")
class IndexController : Resource() {

    @GET
    fun get(){
        getIp()
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET
    public void get(){
        getIp();
    }

}
````

## 获取客户端支持的语言

````kotlin
@API("/")
class IndexController : Resource() {

    @GET
    fun get(){
        lang()
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET
    public void get(){
        lang();
    }

}
````

## 获取Body

Cloudopt Next支持自动将Body转为JSON或者JSONArray，使用内置的Jsoner进行转换。建议在使用Cloudopt Next期间处理JSON都通过Jsoner工具类。具体见[Json](/zh-cn/json.md)一章。同时还支持获取到Json字符串后自动反序列化为对象。

````kotlin
@API("/")
class IndexController : Resource() {

    @GET
    fun get(){
        getBody()
        getBodyString()
        getBodyJson()
        getBodyJson(TestBean::class.java)
        getBodyJsonArray()
        getBodyJsonArray(TestBean::class.java)
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET
    public void get(){
        getBody();
        getBodyString();
        getBodyJson();
        getBodyJson(TestBean.class);
        getBodyJsonArray();
        getBodyJsonArray(TestBean.class);
    }

}
````

## Render

Render系列方法是用于输出请求结果的方法，具体可见[Render](/zh-cn/render.md)一章。

## 输出文件

````kotlin
@API("/")
class IndexController : Resource() {

    @GET
    fun get(){
        sendFile(文件名)
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET
    public void get(){
        sendFile(文件名);
    }

}
````

## 跳转

````kotlin
@API("/")
class IndexController : Resource() {

    @GET
    fun get(){
        redirect("/a")
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET
    public void get(){
        redirect("/a");
    }

}
````

## 报错

fail方法用于强行引发HTTP请求错误，当发生HTTP请求错误时Cloudopt Next会自动调用默认的[错误拦截](/zh-cn/error-handler.md)。

````kotlin
@API("/")
class IndexController : Resource() {

    @GET
    fun get(){
        fail(400)
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET
    public void get(){
        fail(400);
    }

}
````

## 获取上传的文件

Cloudopt Next是基于vertx-web的，vertx-web在获取到用户上传的文件时会自动改名并存放，所以Cloudopt Next也延续了这个功能。当用户上传文件时，Cloudopt Next会自动改名并存放在上传文件目录，路由中能拿到的只有FileUpload对象列表。

````kotlin
@API("/")
class IndexController : Resource() {

    @POST
    fun post() {
       var files = getFiles()
        files?.forEach { file->
            println("-------------------------------------")
            println("FileName: ${file.fileName()}")
            println("UploadedFileName: ${file.uploadedFileName()}")
            println("ContentType: ${file.contentType()}")
            println("-------------------------------------")
        }

        renderText("success!")
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @POST
    public void post(){
        Set<FileUpload> files = getFiles();
        files.forEach(file->{
            System.out.println("-------------------------------------");
            System.out.println("FileName: ${file.fileName()}");
            System.out.println("UploadedFileName: ${file.uploadedFileName()}");
            System.out.println("ContentType: ${file.contentType()}");
            System.out.println("-------------------------------------");
        });
    }

}
````

## 参数注入

自 `2.0.6.0-BETA` 版本后支持直接声明在参数中即可。同时会根据有参方法和无参方法自动跳过参数校验，以免反射扫描降低性能。使用时请先引入 `cloudopt-next-validator` 插件。

````kotlin
    @GET("args")
    fun argsController(
        @Parameter("name", defaultValue = "Peter")
        name: String,
        @Parameter("age")
        age: Int
    ) {
        var map = hashMapOf<String, Any>()
        map["name"] = name
        map["age"] = age
        renderJson(map)
    }
````

你可以通过 `@Parameter` 注解指定参数名称，在用户发送 http 请求时自动将参数注入。或者使用 `@RequestBody` 注解将整个 body 作为 json 字符串并转为对象注入。同时还支持在参数上直接声明参数校验的注解，会自动校验参数。如果参数校验发现问题会自动发生 400 状态码错误并且将验证器上的错误信息自动放入 resource 对象中的上下文对象 context 的 data 中，可以通过自定义的错误拦截器进行拦截。

````kotlin
    val errorMessage = if(context.data().containsKey("errorMessage")){
            context.data()["errorMessage"].toString()
        }else{
            "This is a bad http request, please check if the parameters match the requirements."
        }
        renderJson(restult(errorStatusCode.toString(),errorMessage))
````