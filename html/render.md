## Use Render

Render is syntactic sugar that has been written in the Resource class. When you need to output something, you can call the method directly. Currently supported views are Html, Json, Text, FreeMaker, Hbs. These types can be used directly in the Resource.

It should be noted that FreeMaker, Hbs all need to refer to their dependencies. Cloudopt Next does not. More code examples can be found at [GitHub](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-web/src/test/java/net/cloudopt/next/web/test/ Controller/IndexController.kt).

When rendering the page, Render automatically reads the file according to the configuration of the templates item in the configuration file. The default is in the templates folder.


## Create your own Render

If you need to use a template engine that is not yet supported by Cloudopt Next, you can write a Render yourself. Suggested reference [Json Render](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-web/src/main/java/net/cloudopt/next/web/render/JsonRender.kt) .

After creating a Java class, add it before the server starts.

````kotlin
CloudoptServer.addRender("custom",JsonRender())
````

````java
CloudoptServer.addRender("custom",new JsonRender());
````

When you use it, you only need to add a name to the route.

````kotlin
render("custom","text")
````

````java
render("custom","text");
````

## Modify the default Render

By default, JsonRender is automatically called if the render method is called directly. If you need to modify the default Render, you need to call the RenderFactory to edit it.

````kotlin
RenderFactory.setDefaultRender("json")
````

````java
RenderFactory.INSTANCE.setDefaultRender("json");
````

## Static resources

The static resource files such as CSS, JS, and pictures are separated from the template file. By default, they are placed in the static folder. When the page needs to refer to a static data, the static file can be directly referenced.

````html
<link rel="shortcut icon" href="/static/favicon.ico" type="image/x-icon"/>
````
