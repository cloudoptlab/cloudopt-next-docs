cloudopt-next-i18n is an easy and convenient internationalization plugin. All you need to do is prepare the corresponding language JSON file in the `_locales` folder under the `resources` folder.

Please refer to the appropriate dependencies before using it. Please add your own version number.

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

It is then only necessary to obtain the corresponding value by means of the I18N class. The first parameter is the keyword in the language file and the second parameter is the name of the language file.

````kotlin
I18N.i18n("title", "en")
````

You can also get a deeper level of translation by way of a.b.c.

````kotlin
I18N.i18n("meta.author.name", "en")
````