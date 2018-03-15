[jOOQ](http://www.jooq.org/)is a toolkit for writing SQL based on Java. It has the unique advantages of simple, lightweight, functional programming and writing SQL, and is very suitable for agile and rapid iterative development. It is also the Orm recommended by Cloudopt Next.

Cloudopt Next provides a plug-in to jOOQ for easy startup of Jooq. You only need to configure the datasource and jooq in the Cloudopt Next configuration file.

Please refer to the appropriate dependencies before use. If you do not inherit cloudopt-next-parent, please add the version number yourself.

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
| jdbcUrl| Database connection address.      |
| username| Database username.      |
| password| Database password.      |
| driverClassName| Database connection driver name.      |
| pool| The class name of the connection pool implementation class.      |
| database| The database name used. Specific support to fill in the parameters see the following table.    |

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

Adding a plugin before the server is started automatically creates a connection pool and initializes the Jooq.

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

If you need to use other connection pools, you can refer to [HikariCPPool](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-jooq/src/main/java/net/cloudopt/next/ Jooq/pool/HikariCPPool.kt) Implement and modify the configuration.