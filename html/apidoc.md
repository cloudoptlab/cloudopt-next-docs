We recommend using apidoc as the automatic generation tool of API documents. Although many people will use swagger, I think the code of swagger is relatively invasive. We hope that the project based on cloudopt next is as simple as possible with as little code. So after a long period of research, we think [apidoc] is recommended (https://github.com/apidoc/apidoc)

Document: [apidocjs. Com] (http://apidocjs.com)

[example] (http://apidocjs.com/example/) output

Installation of cable vehicles

```bash

$ npm install -g apidoc

` ` ` `

The use of add a similar comment on the routing method:

```java

* *

* @api {get} /user/:id Request User information

* @apiName GetUser

* @apiGroup User

*

* @apiParam {Number} id User's unique ID.

*

* @apiSuccess {String} firstname Firstname of the User.

* @apiSuccess {String} lastname Lastname of the User.

* /

```

Now we scan all files in the `src/` folder and output the results to `doc/`

```bash
$ apidoc -i src/ -o doc/
```

If you are kotlin and want to visit the same website, you can use the following methods:

```bash

apidoc -f ".*\\.kt$" -i src/main/kotlin/ -o src/main/resources/static/apidoc

```

Next you can access it through `http://localhost:8080/static/apidoc`.