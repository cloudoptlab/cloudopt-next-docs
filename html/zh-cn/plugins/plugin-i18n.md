cloudopt-next-i18n 是个简易的方便的国际化插件。你只需要在 `resources` 文件夹下的 `_locales` 文件夹中准备相应的语言 json 文件即可。

在使用前请先自行引用相应的依赖。请自行添加版本号。

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-i18n</artifactId>
</dependency>
````


en.json
````json
{
  "title": "This is English title.",
  "meta": {
    "author": {
      "name": "cloudopt",
      "email": "support@cloudopt.net"
    }
  }
}
````

然后只需要通过 I18N 类的方法获取相应的值即可。第一个参数是在语言文件中的关键字，第二个参数是语言文件名称。

````kotlin
I18N.i18n("title", "en")
````

你还可以通过 a.b.c 的方式获取更深层级的翻译。

````kotlin
I18N.i18n("meta.author.name", "en")
````