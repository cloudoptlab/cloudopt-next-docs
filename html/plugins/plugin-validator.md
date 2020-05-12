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
}

Account account=new Account()
account.validation() //Verify all parameters
account.getErrorMessage()  //To obtain the error message is to verify the message content on the failed annotation
account.validation("password", "username") //Verify only some parameters
````

> The supported annotations can be referred to：https://docs.jboss.org/hibernate/stable/validator/reference/en-US/html_single/#validator-defineconstraints-spec
