当发生错误时，Cloudopt Next将会自动调用错误拦截器进行处理。默认的错误拦截器[DefaultErrorHandler](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-web/src/main/java/net/cloudopt/next/web/handler/DefaultErrorHandler.kt)会拦截404和500错误并输出错误信息。

如果您需要处理更多错误，可以模仿DefaultErrorHandler创建一个Handler，并在配置文件中修改相应的配置即可。