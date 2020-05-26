cloudopt-plugin-auth 是一个轻量级的权限校验框架，对 restful 友好，支持通配符。插件将权限分为三个级别：组、角色、用户三个级别，默认通过 json 文件进行配置。你还可以自行继承 `Auth` 类实现自定义从数据库中获取或者从其它文件中获取。实现类可以参考 [`JsonAuth`](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-auth/src/main/kotlin/net/cloudopt/next/auth/impl/JsonAuth.kt) 这个类是如何实现的。

在使用前请先自行引用相应的依赖，请自行添加版本号。

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-auth</artifactId>
</dependency>
````

如果你使用的是默认的权限校验，可以直接在 `application.json` 中配置权限。

````json
{
  "auth": {
    "roles": [
      {
        "id": 1,
        "name": "operate",
        "rules": [
          {
            "name": "about account",
            "url": "/api/v1/account/*",
            "method": "GET",
            "allow": true
          }
        ]
      }
    ],
    "groups": [
      {
        "id": 1,
        "name": "login",
        "rules": [
          {
            "name": "about login",
            "url": "/api/v1/login",
            "method": "POST",
            "allow": true
          }
        ]
      }
    ],
    "users": [
      {
        "id": 1,
        "uniqueTag": "SHUH-OSJI-UHIN-UUHG",
        "rolesIdList": [
          1
        ],
        "groupsIdList": [
          1
        ],
        "rules": [
          {
            "name": "block add account",
            "url": "/api/v1/account/*",
            "method": "POST||DELETE",
            "allow": false
          }
        ]
      }
    ]
  }
}
````

使用时，你只需要传入请求的 url、 method、和用户的唯一标签（可以设置为用户在业务系统的唯一id，自行控制）即可。

````kotlin
var authority: Auth = JsonAuth()
authority.enforce(uniqueTag, "/api/v1/account/creat", "GET")
authority.enforce(uniqueTag, "/api/v1/account/creat", "POST")
authority.enforce(uniqueTag, "/api/v1/push", "POST")
````
