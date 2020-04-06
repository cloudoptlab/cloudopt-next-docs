我们推荐使用 apidoc 作为 api 文档的自动生成工具，虽然很多人会使用 swagger，个人认为 swagger 的代码入侵性比较强，我们希望基于 cloudopt-next 项目是尽量少的代码、尽量简单的项目。所以我们再经过很长一段时间的调研后觉得推荐 [apidoc](https://github.com/apidoc/apidoc)

文档: [apidocjs.com](http://apidocjs.com)

[示例](http://apidocjs.com/example/) output.

## 安装

```bash
$ npm install -g apidoc
```

## 使用

在路由方法上添加类似的注释:

```java
/**
 * @api {get} /user/:id Request User information
 * @apiName GetUser
 * @apiGroup User
 *
 * @apiParam {Number} id User's unique ID.
 *
 * @apiSuccess {String} firstname Firstname of the User.
 * @apiSuccess {String} lastname  Lastname of the User.
 */
```

我们现在扫描 `src/` 文件夹下的所有文件并将结果输出到 `doc/`.

```bash
$ apidoc -i src/ -o doc/
```

如果你是 Kotlin ，并且希望在同一个网站访问的话你可以用下面的方法：

```bash
apidoc -f ".*\\.kt$" -i src/main/kotlin/ -o src/main/resources/static/apidoc
```

接下来你可以通过 `http://localhost:8080/static/apidoc` 访问了。