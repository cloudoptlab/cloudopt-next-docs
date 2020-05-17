## Release Notes

The version of Cloudopt Next will use the version number + suffix, for example:，1.0.0-SNAPSHOT. There are generally the following versions of suffixes:

- SNAPSHOT：Test version. Each update may change significantly. There may be more severe BUG.
- BETA：Preview version. Before the official version will enter the BETA stage. This version has already made great progress with respect to SNAPSHOT and is stable a lot, but there may still be problems.
- RELEASES：Official version. After long-term testing, there are generally no significant problems.

The version number is generally three, and each update will change the version number according to the specific update content. If only the BUG is fixed, it will just change the third place, such as, 1.0.1. The addition of new features (including removal of old elements) and other major changes will improve the second version number. If there are very extensive changes that may not be compatible with the previous version, the first version number will be modified.

The current latest version is: `2.0.3.8-BETA`.

## System Requirements

Cloudopt Next requires that the JDK must be 1.8 or later.

## Maven

### Add repository

For Maven, using cloudopt-next must introduce the corresponding source, you need to modify the project pom.xml and add the following code:

````xml
<repositories>
    <repository>
        <id>cloudopt-center</id>
        <url>https://dl.bintray.com/cloudopt/maven</url>
    </repository>
</repositories>
````

### Adding dependencies

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-web</artifactId>
    <version>${version}</version>
</dependency>
````

>Complete pom.xml example can access[GitHub](https://github.com/cloudoptlab/cloudopt-next-example/blob/master/pom.xml)view。

## Gradle

For Gradle, using cloudopt-next must introduce the corresponding source, you need to modify the project build.gradle and add the following code:

```groovy
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