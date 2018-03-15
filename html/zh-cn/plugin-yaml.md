不建议直接使用。

在使用前请先自行引用相应的依赖。如果您并没有继承cloudopt-next-parent的话，请自行添加版本号。

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-yaml</artifactId>
</dependency>
````

````kotlin
fun test() {
    println(Yamler.read("application.yml","net.cloudopt.next"))
    var yaml:YamlBean= Yamler.read(YamlBean::class) as YamlBean
    //If you want to use the kotlin data class in the JVM,
    // the parameters of the data class must have default values.
    println(yaml.toString())
}

fun testReadFileList(){

    var map = linkedMapOf<String, Any>()

    if (Yamler.read("application.yml") != null) {
        map.putAll(Yamler.read("application.yml") as Map<out String, Any>)
    }

    if (Yamler.read("application-dev.yml") != null) {
        map.putAll(Yamler.read("application-dev.yml") as Map<out String, Any>)
    }

    if (Yamler.read("application-pro.yml") != null) {
        map.putAll(Yamler.read("application-pro.yml") as Map<out String, Any>)
    }

    println(map.toString())
}
````