## Create an Intercept

Intercept is an interceptor for @API annotations that acts on the entire class. Let's take a look at a simple example.

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

After creating a class, you need to implement the Interceptor class. When the request comes in, it will automatically execute the contents of the intercept method. If it returns false, it will automatically execute the response method. If it returns true, it will enter the next stage.

## Use Interceptor

Using Interceptor is also very simple, just configure it in the @API annotation.

````kotlin
@API("/",interceptor = arrayOf(TestInterceptor::class))
````

````java
@API(value = "/",interceptor = {TestInterceptor.class})
````