This document describes how to set protected branches.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. Select **Code Repositories** in the menu on the left and click **Branches** to go to the branch management page.

Branch protection is a special function CODING uses to limit Git code permissions. Selected branches can be protected from unreported and unauthorized changes.

When you enable branch protection, protected branches are marked with a green shield in the branch list. To modify a protected branch, members must create a new branch and modify it. Then, they submit a merge request to invite other members to review the code. If the review result is Allow Merge, the merge operation can be performed.
![](https://qcloudimg.tencent-cloud.cn/raw/d9f55c7eb716f126483c7ab46f30c568.png)

## Set Protected Branch Rules[](id:protected-branch)
In a code repository, go to **Settings** > **Branch Settings**. There, you can use **wildcards** to intelligently set protected branches. Branches that match the set name rules are judged to be protected branches.
![](https://qcloudimg.tencent-cloud.cn/raw/2ee368da44d75588d594af848532caf5.png)

- **Disallow Force Push:** Enabled by default. Even users with permission to perform git push cannot use git push -f to force modify the branch commit history. We strongly recommend you enable this option when multiple people collaborate on a branch. This ensures that users must use new commits to change the branch history, rather than modifying previous commits.
- **Enable Status Check:** By setting the specification check conditions or setting a code scanning scheme in the CI, merges are allowed only after the CI is successful. For more information, see [Continuous Integration > Trigger Rules](https://help.coding.net/docs/ci/configuration/trigger.html).
- **Automatically Add Branch Admin as Reviewer:** When this option is enabled, the relevant branch admins are automatically set as reviewers for all merge requests involving protected branches. When the number of branch admins exceeds the **Number of Reviewers Authorizing Merge**, an appropriate number of reviewers are randomly selected from among the branch admins. For example, if there are three branch admins and the number of reviewers is 2, the system randomly selects two of the three admins as reviewers.
- **Enable Review by Code Owner:** When this option is enabled, for merge requests involving protected branches, any modification must be reviewed by the relevant code owner before the merge is allowed. For more information, see [Code Owner](https://intl.cloud.tencent.com/document/product/1132/44717).
- **Number of Reviewers Authorizing Merge:** This is used to set the number of branch admins that must authorize a merge request. If no branch admins are set for a protected branch, a merge request must be authorized by one ordinary member before the merge is allowed.

## Specify Branch Admins
Branch Admin is optional. After an admin is added, the admin must Allow Merge for every merge request. By default, admins are restricted by the conditions of protected branches, and they need to create merge requests to modify the branches. Select **Allow Direct Push** to allow admins to directly modify the content of protected branches.
![](https://qcloudimg.tencent-cloud.cn/raw/d77c887bb46b38b651b76c7aa506b718.png)
If members do not have permissions for a branch (e.g., when they are not admins of a protected branch), they will receive the following error message when they try to push to this branch.
![](https://qcloudimg.tencent-cloud.cn/raw/34af6f3135264241763e5cd9671ee3dc.png)