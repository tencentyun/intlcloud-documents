This document describes how to adjust the settings of merge requests in a code repository.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, click **Code Repositories** > **Merge Requests**.

Project admins can configure the basic settings as well as default merge modes and target branches of merge requests in **Settings** > **Merge Requests**.
![](https://qcloudimg.tencent-cloud.cn/raw/4723dee8d862973c1abd1751e3eda229.png)

## Delete Source Branch by Default[](id:delete-source-branch)

If this is enabled, the source branch will be deleted after it is merged into the target branch.

## Fast-Forward Merge by Default[](id:fast-forward)

If this is enabled, when there is a direct linear path from the source branch to the target branch, the source branch will directly point to the target branch without a merge commit. This process is called the fast-forward merge.

## Merge Mode[](id:merge-method)

Three merge modes are available for a source branch with multiple commits:

-   Direct Merge by Default: Creates a merge commit.
-   Squash Merge by Default: Combines multiple commits of a source branch into one commit, which can be canceled by users.
-   Only Squash Merge: Force combines multiple commits of a source branch into one commit, which cannot be canceled.

## Default Target Branch[](id:default-branch)

The default target branch for merge requests. We recommend you set the master branch as the default target branch for merge requests.
