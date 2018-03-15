## 版本说明

目前Cloudopt Next处于测试阶段，并未发布正式版本，不过您可以使用SNAPSHOT版本。

Cloudopt Next的版本将会采用版本号+尾缀的方式，如：1.0.0-SNAPSHOT。一般会有以下版本尾缀：

- SNAPSHOT：测试版本，每次更新变动可能较大。可能存在较为严重的BUG。
- BETA：预览版本，在正式版本之前会先进入BETA阶段。该版本相对于SNAPSHOT已经有了很大的进步，稳定了很多，但是仍然可能存在问题。
- RELEASES：正式版本，经过长期的测试，一般不存在重大的问题。

版本号一般都是三位，每次更新将根据具体的更新内容来变更版本号。如果只是修复BUG的话只会变更第三位，如：1.0.1。增加了新的特性（包括去掉旧特性）等等较大的变动会改变第二位版本号。如果有非常大的变动可能与之前的版本都不兼容将会修改第一位版本号。

## 系统要求

Cloudopt Next要求JDK必须是1.8或以上版本。

## 引入SNAPSHOT源

对于Maven来说，使用SNAPSHOT版本必须引入相应的源，您需要修改项目的pom.xml并添加以下代码：

````xml
<repositories>
    <repository>
        <id>oss-snapshots</id>
        <url>https://oss.sonatype.org/content/repositories/snapshots</url>
        <releases>
            <enabled>false</enabled>
        </releases>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
    </repository>
</repositories>
````

## 继承Parent

修改项目的pom.xml添加以下代码：

````xml
<parent>
    <artifactId>cloudopt-next-parent</artifactId>
    <groupId>net.cloudopt.next</groupId>
    <version>1.0.0-SNAPSHOT</version>
</parent>
````

继承了Parent后引入Cloudopt Next的任意组件都将不再需要设置版本号。

## 添加依赖

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-web</artifactId>
</dependency>
````

## 不继承Parent

如果您并不想继承Parent的话，您可以自行添加版本号，如：

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-web</artifactId>
    <version>1.0.0-SNAPSHOT</version>
</dependency>
````

>完整的pom.xml例子可以访问[GitHub](https://github.com/cloudoptlab/cloudopt-next-example/blob/master/pom.xml)查看。