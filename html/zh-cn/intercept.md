## 创建一个Intercept

Intercept是用于放在@API注解里的拦截器，作用于整个类。让我们来看下一个简单的例子吧。

````kotlin
class TestInterceptor : Interceptor {

    override fun intercept(resource: Resource): Boolean {
        println("Through the intercept!")
        return true
    }

    override fun response(resource: Resource): Resource {
        return resource
    }


}
````

````java
public class TestInterceptor implements Interceptor {
    @Override
    public boolean intercept(Resource resource) {
        System.out.println("Through the intercept!");
        return true;
    }

    @NotNull
    @Override
    public Resource response(Resource resource) {
        return resource;
    }
}
````

创建一个类后需要实现Interceptor类，当请求进来时会自动执行intercept方法中的内容，如果里面返回false则会自动执行response方法，如果返回true则进入下一阶段。

## 使用Interceptor

使用Interceptor也非常简单，只需要在@API注解中配置下即可。

````kotlin
@API("/",interceptor = arrayOf(TestInterceptor::class))
````

````java
@API(value = "/",interceptor = {TestInterceptor.class})
````