## 创建一个Validator

Validator是Cloudopt Next的校验组件，主要用于RESTful注解上，与Intercept使用方法类似。

````kotlin
class TestValidator : Validator {

    override fun validate(resource: Resource): Boolean {
        return true
    }

    override fun error(resource: Resource) {
        resource.renderText("error")
    }


}
````

````java
public class TestInterceptor implements Interceptor {

    @Override
    public boolean validate(Resource resource) {
        return true;
    }

    @NotNull
    @Override
    public void error(Resource resource) {
        resource.renderText("error");
    }
}
````

## 使用Validator

````kotlin
@GET(valid = arrayOf(TestValidator::class))
````

````java
@GET(value = "/",valid = {TestValidator.class})
````