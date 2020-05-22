我们推荐使用 docker 进行部署，同时也准备好了三个基础的 docker 镜像 `cloudopt/cloudopt-next-docker:jdk8` 和 `cloudopt/cloudopt-next-docker:jdk10` 、 `cloudopt/cloudopt-next-docker:jdk11-openj9-node12` 帮助大家简化部署过程。所有镜像都已经安装了 node12。

首先你需要设置 maven 的配置，指定用于运行的 main 方法文件，然后在打包成 jar 后，执行这个 jar 就会执行这个方法。

````xml
<plugin>
    <artifactId>maven-assembly-plugin</artifactId>
    <version>3.1.0</version>
    <configuration>
        <!-- 这个archive以及archive里面的设置很重要，没有这个配置，就无法生成可执行jar文件 -->
        <finalName>cloudopt-demo</finalName>
        <archive>
            <manifest>
                <mainClass>net.cloudopt.demo.AppKt</mainClass>
            </manifest>
        </archive>
        <!-- 这个jar-with-dependencies是这个插件中预置的，不用管它，尽管用就好了 -->
        <!-- 当然，你也可以用自己的descriptor。如何用？自己去查这个插件的文档 -->
        <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
        </descriptorRefs>
    </configuration>
    <executions>
        <execution>
            <id>make-assembly</id>
            <!-- 这里的phase和goals都是maven的基础概念，不懂的可以去看maven的文档 -->
            <!-- 总之，当你install你的project的时候，是会涵盖package phase和single goal的 -->
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>
````

然后在 Dockerfile 中配置以下的内容，建议自己修改一下（jar的文件名是根据上面 maven 的配置自动生成的）：

````dockerfile
FROM cloudopt/cloudopt-next-docker:jdk8

RUN rm -rf /project/*

ADD pom.xml /tmp/build/

ADD src /tmp/build/src

RUN mkdir -p /project/

RUN cd /tmp/build && mvn clean install -DskipTests \
    && mv target/cloudopt-network-jar-with-dependencies.jar /project/application.jar \
    && cd / && rm -rf /tmp/build

# Expose port 8080
EXPOSE 8080

CMD ["java","-jar","/project/application.jar"]


````