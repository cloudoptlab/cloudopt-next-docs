cloudopt-next-quartz is a plug-in for you to use the quartz timer. Although vertx has its own timer, the timer is simpler and less powerful than quartz.

Please refer to the corresponding dependency before using. Please add your own version number.

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-quartz</artifactId>
</dependency>
````

````java
var plugin = QuartzPlugin()
val job = JobBean()
job.jobClass = "net.cloudopt.next.quartz.test.Task1"
job.cronExpression = "* * * * * ? *"
job.jobGroup = "TaskJob"
job.jobDesc = "TaskJob"
plugin.addJob(job)
CloudoptServer.addPlugin(plugin)
CloudoptServer.run()
````