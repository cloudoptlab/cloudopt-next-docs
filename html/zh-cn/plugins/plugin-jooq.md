[jOOQ](http://www.jooq.org/)是一个基于 Java 编写 SQL 的工具包，具有：简单、轻量、函数式编程写 SQL 等独特优势，非常适合敏捷快速迭代开发。也是 Cloudopt Next 推荐的 orm。

Cloudopt Next 提供了对 jOOQ 的插件，用于方便启动 jOOQ 。您只需要在 Cloudopt Next 的配置文件中配置下 datasource 和jooq即可。

Cloudopt Next 的 jOOQ 插件默认是使用 HikariCPPool 作为连接池的，如果您需要使用其它连接池，可以参照[HikariCPPool](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-jooq/src/main/java/net/cloudopt/next/jooq/pool/HikariCPPool.kt)进行实现并修改配置。

在使用前请先自行引用相应的依赖，请自行添加版本号。

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-jooq</artifactId>
</dependency>
````

````json
{
  "datasource": {
    "jdbcUrl": "jdbc:mysql://127.0.0.1:8889/cloudopt?useUnicode=true&character_set_server=utf8mb4&serverTimezone=UTC&useSSL=false&allowPublicKeyRetrieval=true",
    "username": "root",
    "password": "root",
    "driverClassName": "com.mysql.cj.jdbc.Driver"
  },
  "jooq": {
    "pool": "net.cloudopt.next.jooq.pool.HikariCPPool",
    "database": "mysql"
  }
}
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
| cubrid|
| derby|
| firebird|
| mariadb|
| postgres|
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

为了方便大家使用，内置了一个简单的分页器，可以体验一下。

````kotlin
JooqPaginate(Jooqer.dsl?.selectFrom(Tables.XXXX)?.where(XXXXXX.KEY.eq(id))!!,20,page).find(XXXXX::class.java)
````