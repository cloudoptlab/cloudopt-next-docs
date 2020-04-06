[jOOQ](http://www.jooq.org/) is a toolkit for writing SQL based on Java. It has the unique advantages of simple, lightweight, functional programming and writing SQL, and is very suitable for agile and rapid iterative development. It is also the Orm recommended by Cloudopt Next.

Cloudopt Next provides a plug-in to jOOQ for easy startup of jOOQ. You only need to configure the data source and jOOQ in the Cloudopt Next configuration file.

The jooq plug-in of cloudopt next uses HikariCPPool as the connection pool by default. If you need to use other connection pools, you can refer to [HikariCPPool] (https://github.com/cloudopt/cloudopt-next/blob/master/cloudopt-next-jooq/src/main/java/net/cloudopt/next/jooq/pool/hikaricpppool.kt) to implement and modify the configuration.

Please refer to the appropriate dependencies before use, please add the version number yourself.

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
| jdbcUrl| Database connection address.      |
| username| Database username.      |
| password| Database password.      |
| driverClassName| Database connection driver name.      |
| pool| The class name of the connection pool implementation class.      |
| database| The database name used. Specific support to fill in the parameters see the following table.    |

| Database     |
|:--------:|
| mysql|
| cubrid|
| derby|
| firebird|
| mariadb|
| postgres|
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