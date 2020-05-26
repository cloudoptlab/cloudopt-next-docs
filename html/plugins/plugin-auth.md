cloudopt-plugin-auth is a lightweight permission validation framework that is restful-friendly and supports wildcards. The plug-in divides permissions into three levels: group, role, and user, which are configured by default via a JSON file. You can also inherit `Auth` class implementations to customize them from the database or from other files. The implementation class can be found in [`JsonAuth`](https://github.com/cloudoptlab/cloudopt-next/blob/master/cloudopt-next-auth/src/main/kotlin/net/cloudopt/next/auth/impl/JsonAuth.kt) How this class is implemented.

Please add your own version number before using it.

Translated with www.DeepL.com/Translator (free version)

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-auth</artifactId>
</dependency>
````

If you are using the default permission checksum, you can configure permissions directly in `application.json`.

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

To use, all you need is the URL of the incoming request, the method, and the user's unique tag (which can be set to the user's unique ID on the business system and controlled by itself).

````kotlin
var authority: Auth = JsonAuth()
authority.enforce(uniqueTag, "/api/v1/account/creat", "GET")
authority.enforce(uniqueTag, "/api/v1/account/creat", "POST")
authority.enforce(uniqueTag, "/api/v1/push", "POST")
````
