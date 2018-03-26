## Release Notes

Cloudopt Next is currently in beta and there is no official release, but you can use the SNAPSHOT version.

The version of Cloudopt Next will use the version number + suffix, for example:，1.0.0-SNAPSHOT. There are generally the following versions of suffixes:

- SNAPSHOT：Test version. Each update may change significantly. There may be more severe BUG.
- BETA：Preview version. Before the official version will enter the BETA stage. This version has already made great progress with respect to SNAPSHOT and is stable a lot, but there may still be problems.
- RELEASES：Official version. After long-term testing, there are generally no significant problems.

The version number is generally three, and each update will change the version number according to the specific update content. If only the BUG is fixed, it will just change the third place, such as, 1.0.1. The addition of new features (including removal of old elements) and other major changes will improve the second version number. If there are very extensive changes that may not be compatible with the previous version, the first version number will be modified.

## System Requirements

Cloudopt Next requires that the JDK must be 1.8 or later.

## Introduce SNAPSHOT source

For Maven, using SNAPSHOT version must introduce the corresponding source, you need to modify the project pom.xml and add the following code:

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

## Inherit the Parent

Modify the pom.xml of the project by adding the following code:

````xml
<parent>
    <artifactId>cloudopt-next-parent</artifactId>
    <groupId>net.cloudopt.next</groupId>
    <version>1.0.0-SNAPSHOT</version>
</parent>
````

Any component that introduces Cloudopt Next after inheriting the Parent will no longer need to set the version number.

## Adding dependencies

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-web</artifactId>
</dependency>
````

## Does not inherit Parent

If you do not want to inherit from the Parent, you can add the version number yourself, such as:

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-web</artifactId>
    <version>1.0.0-SNAPSHOT</version>
</dependency>
````

>Complete pom.xml example can access[GitHub](https://github.com/cloudoptlab/cloudopt-next-example/blob/master/pom.xml)view。