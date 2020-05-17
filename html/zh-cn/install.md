## 版本说明

Cloudopt Next的版本将会采用版本号+尾缀的方式，如：1.0.0-SNAPSHOT。一般会有以下版本尾缀：

- SNAPSHOT：测试版本，每次更新变动可能较大。可能存在较为严重的BUG。
- BETA：预览版本，在正式版本之前会先进入BETA阶段。该版本相对于SNAPSHOT已经有了很大的进步，稳定了很多，但是仍然可能存在问题。
- RELEASES：正式版本，经过长期的测试，一般不存在重大的问题。

版本号一般都是三位，每次更新将根据具体的更新内容来变更版本号。如果只是修复BUG的话只会变更第三位，如：1.0.1。增加了新的特性（包括去掉旧特性）等等较大的变动会改变第二位版本号。如果有非常大的变动可能与之前的版本都不兼容将会修改第一位版本号。

目前的最新版本是：`2.0.3.8-BETA`。

## 系统要求

Cloudopt Next要求JDK必须是1.8或以上版本。

## Maven

### 增加仓库

对于 Maven 来说，使用 cloudopt-next 版本必须引入相应的源，您需要修改项目的 pom.xml 并添加以下代码：

````xml
<repositories>
    <repository>
        <id>cloudopt-center</id>
        <url>https://dl.bintray.com/cloudopt/maven</url>
    </repository>
</repositories>
````

## 添加依赖


````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-web</artifactId>
    <version>${version}</version>
</dependency>
````

>完整的pom.xml例子可以访问[GitHub](https://github.com/cloudoptlab/cloudopt-next-example/blob/master/pom.xml)查看。

## Gradle

### 增加仓库

对于 Gradle 来说，使用 cloudopt-next 版本必须引入相应的源，您需要修改项目的 build.gradle 并添加以下代码：

```gradle
repositories {
    maven {
        url  "https://dl.bintray.com/cloudopt/maven" 
    }
}
```

### Adding dependencies

````groovy
dependencies{
    implementation "net.cloudopt.next:cloudopt-next-web:$version"
}
````