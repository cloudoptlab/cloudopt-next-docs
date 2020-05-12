cloudopt-next-validator 是 Cloudopt Next 自带的一个优雅的数据校验器，你只需要在 pojo 类需要校验的字段上增加相应的注解即可。

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-validator</artifactId>
</dependency>
````

````java
public class Account(){
    @NotNull(message="如果message里面包含了文字，那么出错时可以获取得到")
    private String test;
}

Account account=new Account()
account.validation() //校验所有参数
account.getErrorMessage()  //获取出错信息，就是校验失败的注解上message的内容
account.validation("password", "username") //只校验某些参数
````

目前已经自带了以下的注解：

````java
//用于boolean字段，该字段只能为true。
@AssertTrue

//该字段的值只能为false。
@AssertFalse

//对信用卡号进行一个大致的验证。
@CreditCardNumber

//只能小于或等于该值。
@DecimalMax  

//只能大于或等于该值。
@DecimalMin

//检查是否是一种数字的整数、分数,小数位数的数字。
@Digits(integer=2,fraction=20)

//检查是否是一个有效的email地址。
@Email

//检查该字段的日期是否是属于将来的日期。
@Future

//检查所属的字段的长度是否在min和max之间,只能用于字符串。
@Length(min=1,max=3)

//该字段的值只能小于或等于该值。
@Max(value = 4)

//该字段的值只能大于或等于该值。
@Min(value = 4)

//不能为null。
@NotNull

//不能为空,检查时会将空格忽略。
@NotBlank

//不能为空，这里的空是指空字符串。
@NotEmpty

//检查该字段为空。
@Null

//检查该字段的日期是在过去。
@Past

//检查该字段的size是否在min和max之间，可以是字符串、数组、集合、Map等。
@Size(min=1, max=3)

//检查是否是一个有效的URL，如果提供了protocol，host等，则该URL还需满足提供的条件。
@URL(protocol=,host,port)

//如果使用这个注解，那么该变量中包含的对象如果也有校验器注解的话就会自动进行校验。
@Valid

//检查是否是信用卡卡号
@CreditCardNumber(ignoreNonDigitCharacters=)

//是否是个链接
@URL(protocol=, host=, port= regexp=, flags=)

//是否是boolean或者int或者double，根据所需在value那里传入即可。如value="boolean"
@Type(value=)

//是否在这个数组（字符串）中
@Inside(value={})

//是否是中文或者不是中文。如果为true则要求变量必须是中文，如果为false则要求变量不能为中文
@Chinese(value=boolean)
````

> 更多支持的注解可以参考：https://docs.jboss.org/hibernate/stable/validator/reference/en-US/html_single/#validator-defineconstraints-spec