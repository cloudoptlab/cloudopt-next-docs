We recommend using docker for deployment. At the same time, we have prepared three basic docker images: `cloudopt/cloudopt-next-docker:jdk8` and `cloudopt/cloudopt-next-docker:jdk10` and `cloudopt/cloudopt-next-docker:jdk11-openj9-node12` to help you simplify the deployment process. All images have node12 installed.

First of all, you need to set the configuration of maven, specify the main method file to run, and then after packaging into jar, execute the jar to execute the method.
````xml
<plugin>
    <artifactId>maven-assembly-plugin</artifactId>
    <version>3.1.0</version>
    <configuration>
        <finalName>cloudopt-demo</finalName>
        <archive>
            <manifest>
                <mainClass>net.cloudopt.demo.AppKt</mainClass>
            </manifest>
        </archive>
        <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
        </descriptorRefs>
    </configuration>
    <executions>
        <execution>
            <id>make-assembly</id>
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>
````

Then configure the following contents in the dockerfile. It is recommended to modify them (the file name of the jar is automatically generated according to the above Maven configuration):

````dockerfile
FROM cloudopt/cloudopt-next-docker:jdk8

RUN rm -rf /project/*

ADD pom.xml /tmp/build/

ADD src /tmp/build/src

RUN mkdir -p /project/

RUN cd /tmp/build && mvn clean install -DskipTests \
    && mv target/cloudopt-demo-jar-with-dependencies.jar /project/application.jar \
    && cd / && rm -rf /tmp/build

# Expose port 8080
EXPOSE 8080

CMD ["java","-jar","/project/application.jar"]


````