## 提交 Pull Request

如果你有仓库的开发者权限，而且希望贡献代码，那么你可以创建分支修改代码提交 PR，Cloudopt Next 开发团队会 review 代码合并到主干。

由于谁也无法保证过了多久之后还记得多少，为了后期回溯历史的方便，请在提交 MR 时确保提供了以下信息。

- 需求点（一般关联 issue 或者注释都算）

- 升级原因（不同于 issue，可以简要描述下为什么要处理）

- 框架测试点（可以关联到测试文件，不用详细描述，关键点即可）

- 关注点（针对用户而言，可以没有，一般是不兼容更新等，需要额外提示）

## Commit 提交规范

根据 [angular](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#commit-message-format) 规范提交 commit， 这样 history 看起来更加清晰，还可以自动生成 changelog。

````xml
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
````

（1）type

提交 commit 的类型，包括以下几种:

- feat: 新功能

- fix: 修复问题

- docs: 修改文档

- style: 修改代码格式，不影响代码逻辑

- refactor: 重构代码，理论上不影响现有功能

- perf: 提升性能

- test: 增加修改测试用例

- chore: 修改工具相关（包括但不限于文档、代码生成等）

- deps: 升级依赖

（2）scope

修改文件的范围（包括但不限于 doc, middleware, core, config, plugin）

（3）subject

用一句话清楚的描述这次提交做了什么

（4）body

补充 subject，适当增加原因、目的等相关因素，也可不写。

（5）footer

> 当有非兼容修改(Breaking Change)时必须在这里描述清楚。如果要关联相关 issue需要增加说明，如 Closes #1, Closes #2, #3。