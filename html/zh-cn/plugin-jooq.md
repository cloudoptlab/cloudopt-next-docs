[jOOQ](http://www.jooq.org/)是一个基于Java编写SQL的工具包，具有：简单、轻量、函数式编程写SQL等独特优势，非常适合敏捷快速迭代开发。也是Cloudopt Next推荐的orm。

Cloudopt Next提供了对jOOQ的插件，用于方便启动Jooq。您只需要在Cloudopt Next的配置文件中配置下datasource和jooq即可。

在使用前请先自行引用相应的依赖。如果您并没有继承cloudopt-next-parent的话，请自行添加版本号。

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-jooq</artifactId>
</dependency>
````

````yaml
net:
  cloudopt:
    next:
      datasource:
        jdbcUrl: "jdbc:mysql://localhost:3306/cloudopt_example?useUnicode=true&characterEncoding=UTF-8&serverTimezone=UTC&useSSL=true"
        username: "root"
        password: "root"
        driverClassName: "com.mysql.cj.jdbc.Driver"
      jooq:
        pool: "net.cloudopt.next.jooq.pool.HikariCPPool"
        database: "mysql"
````

| Name     | Description|
|:--------:|:-------|
| jdbcUrl| 数据库连接地址。      |
| username| 数据库用户名。      |
| password| 数据库密码。      |
| driverClassName| 数据库连接驱动名。      |
| pool| 连接池实现类的类名。      |
| database| 使用的数据库名称。具体支持填写的参数见下面的表格。    |

| Database     |
|:--------:|
| mysql|
| mysql 5.7|
| mysql 8.0|
| cubrid|
| derby|
| firebird|
| firebird 2.5|
| firebird 3.0|
| mariadb|
| postgres|
| postgres 9.3|
| postgres 9.4|
| postgres 9.5|
| sqlite|

配置好后在服务器启动前增加插件便会自动创建连接池和初始化Jooq。

````kotlin
fun main(args: Array<String>) {
    CloudoptServer.addPlugin(JooqPlugin())
    CloudoptServer.run(TestCase::class)
}
````

````java
fun main(args: Array<String>) {
    CloudoptServer.addPlugin(JooqPlugin());
    CloudoptServer.run(TestCase.class);
}
````

如果您需要使用其它连接池，可以参照[HikariCPPool](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-jooq/src/main/java/net/cloudopt/next/jooq/pool/HikariCPPool.kt)进行实现并修改配置。