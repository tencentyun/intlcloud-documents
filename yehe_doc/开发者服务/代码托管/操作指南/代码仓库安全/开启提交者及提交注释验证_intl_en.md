This document describes how to enable verification of committers and commit messages in a code repository.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.

Project admins can enable verification of Git committers and authors in **Settings** > **Push Settings**.

![](https://qcloudimg.tencent-cloud.cn/raw/84e60edf2dc3c2fcd89af9192944af3e.png)

Project admins can also set rules for Git commit messages. Commits that do not conform to the rules will be rejected. For example, the rule `^fix #[0-9]+` requires that the commit message must include the associated project issue. `^fix #630` indicates that the commit is associated to issue 630 in the project.

>?To learn how to automatically associate issues in commit messages, see [Committing Files](https://intl.cloud.tencent.com/document/product/1132/44685).
