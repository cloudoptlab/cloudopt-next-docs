Cloudopt Next本身附带了一个建议的Waf插件，Waf可以有效阻止SQL注入攻击、XSS攻击、Mongodb注入攻击，还支持一键开启CSRF防御机制。

cloudopt-next-web与cloudopt-next-waf已经深度整合，无需另外启动插件。

````yaml
net:
  cloudopt:
    next:
      waf:
        plus: true
        csrf: false
        xss: true
        sql: true
        mongodb: true
````

| Name     | Description|
|:--------:|:-------|
| plus| 在动在HTTP Heards中增加安全相关的设置。      |
| csrf| 开启CSRF防御机制，阻止可以访问。      |
| xss| 开启XSS防御。      |
| sql| 开启SQL注入防御。      |
| mongodb| 开启Mongodb注入防御。      |