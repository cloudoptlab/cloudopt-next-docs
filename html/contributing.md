## Pull Request Guide

If you are developer of cloudopt repo and you are willing to contribute, feel free to create a new branch, finish your modification and submit a PR. cloudopt group will review your work and merge it to master branch.

No one can garantee how much will be remembered about certain PR after some time. To make sure we can easily recap what happened previously, please provide the following information in your PR.

- Need: What function you want to achieve (Generally, please point out which issue is related).

- Updating Reason: Different with issue. Briefly describe your reason and logic about why you need to make such modification.

- Related Testing: Briefly descirbe what part of testing is relevant to your modification.

-User Tips: Notice for Cloudopt users. You can skip this part, if the PR is not about update in API or potential compatibility problem.

## Commit Message Format

You are encouraged to use [angular commit-message-format](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#commit-message-format) to write commit message. In this way, we could have a more trackable history and an automatically generated changelog.

````xml
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
````

（1）type

Must be one of the following:

- feat: A new feature

- fix: A bug fix

- docs: Documentation-only changes

- style: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)

- refactor: A code change that neither fixes a bug nor adds a feature

- perf: A code change that improves performance

- test: Adding missing tests

- chore: Changes to the build process or auxiliary tools and libraries such as documentation generation

- deps: Updates about dependencies

（2）scope

The scope could be anything specifying place of the commit change. For example $location, $browser, $compile, $rootScope, ngHref, ngClick, ngView, etc...

（3）subject

Use succinct words to describe what did you do in the commit change.

（4）body

Feel free to add more content in the body, if you think subject is not self-explanatory enough, such as what it is the purpose or reasone of you commit.

（5）footer

> If the commit is a Breaking Change, please note it clearly in this part. related issues, like Closes #1, Closes #2, #3