﻿﻿## Use annotations

The routes in Cloudopt Next are used by annotations. Any class inherits the Resource class and adds @API to the header. 

Such as:

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

Cloudopt Next automatically scans classes containing @API annotations at startup and automatically parses all the methods in the class. The specific principle can refer to chapter [deep-routing principle] (/deep-route.md).

Specific URLs can be set in the @API, and methods in this class will also be automatically inherited.

如：

@API("/")  =>  http://localhost:8080/

@API("/test")  =>  http://localhost:8080/test

## RESTful

Cloudopt Next supports @GET, @POST, @PUT, @DELETE, and @PATCH, which correspond to the five methods in the HTTP request. RESTful-related annotations can only be used on plans, as are the @APIs that support configuring URLs. Cloudopt Next automatically splices URLs set in the @API with URLs configured in RESTful annotations.

Such as:

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

You will need to access via GET http://localhost:8080/hello.

## Get parameters

If you need to get theparameters passed by the client, you can use the getParam() method directly in the method.

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

## Get URL parameters

If you need to get the parameters on the URL, you need to set in the RESTful annotation: parameter name.

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

## Get form datas

If you need to get the form parameters passed by the client, you can get them directly in the method using the getParam() method。

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

## Cookie

Cookie also supports more settings, you can see the parameter annotation of the setCookie method.

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

## Get IP

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

## Get client supported language

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

## Get Body

Cloudopt Next supports automatic body conversion to JSON or JSONArray, using the built-in Jsoner for conversion. It is recommended that the JSON be processed through the Jsoner utility class during the use of Cloudopt Next. See the chapter [Json](/json.md) for details. It also supports the automatic deserialization of objects into Json strings.

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

The Render series method is a method for outputting the result of the request, which can be seen in the chapter [Render](/render.md).

##Output file

````kotlin
@API("/")
class IndexController : Resource() {

    @GET
    fun get(){
        sendFile(file name)
    }

}
````

````java
@API("/")
public class IndexController extends Resource {

    @GET
    public void get(){
        sendFile(file name);
    }

}
````

## Jump

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

## Error

The fail method is used to force an HTTP request error. When an HTTP request error occurs, Cloudopt Next automatically calls the default [error interception](/error-handler.md).

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

##Get uploaded the file

Cloudopt Next is based on vertx-web, vertx-web will automatically rename and store when obtaining user uploaded files, so Cloudopt Next also continues this function. When a user uploads a file, Cloudopt Next automatically renames and saves it in the uploaded file directory. Only the FileUpload object list can be obtained in the route.

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

Since `2.0.6.0-BETA` version, direct declaration in parameters is supported. At the same time, it automatically skips the parameter checks according to the reference and non-reference methods to avoid the reflection scan reduces the performance. Include the `cloudopt-next-validator` plug-in first.

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

You can specify the parameter name in the `@Parameter` comment, which is used when the user sends an http request. Parameters are automatically injected. Or use the `@RequestBody` annotation to merge the entire body as a json string. Switch to object injection. It also supports declaring a parameter-checked comment directly on the parameter, which will check the parameter automatically. If the parameter check finds a problem, a 400 status code error is automatically generated and the error message from the verifier is automatically placed in the The data in the context of the context object in the resource object can be customized with the of the error interceptor to intercept.

````kotlin
    val errorMessage = if(context.data().containsKey("errorMessage")){
            context.data()["errorMessage"].toString()
        }else{
            "This is a bad http request, please check if the parameters match the requirements."
        }
        renderJson(restult(errorStatusCode.toString(),errorMessage))
````