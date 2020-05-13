Cloudopt-next-validator is an elegant data validator provided by Cloudopt Next. You only need to add corresponding annotation on the fields that need to be verified in the POJO class.

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-validator</artifactId>
</dependency>
````

````java
public class Account(){
    @NotNull(message="If the message contains text, you can get it in case of error")
    private String test;
    // get and set
}

Account account=new Account();
ValidatorTool.validate(account); //Verify all parameters and get the error message is to verify the message content on the failed annotation
ValidatorTool.validate(account，"password", "username"); //Verify only some parameters
System.out.println(ValidatorTool.validate(account).getResult());
System.out.println(ValidatorTool.validate(account).getMessage());
````

````kotlin
data class Account(){
    @get:NotNull(message="If the message contains text, you can get it in case of error")
    var test:String=""
}

Account account=new Account()
ValidatorTool.validate(account) //Verify all parameters and get the error message is to verify the message content on the failed annotation
ValidatorTool.validate(account，"password", "username") //Verify only some parameters
println(ValidatorTool.validate(account).result)
println(ValidatorTool.validate(account).message)
````

> The supported annotations can be referred to：https://docs.jboss.org/hibernate/stable/validator/reference/en-US/html_single/#validator-defineconstraints-spec
