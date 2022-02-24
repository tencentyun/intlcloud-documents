This document describes how to set hidden branches.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. Select **Code Repositories** in the menu on the left and click **Branches** to go to the branch management page.

To control access permissions to a single branch, you can make any branch other than the default branch a hidden branch. Only authorized users and user groups can access hidden branches, ensuring the security of the code.

1.  On the details page of a code repository, click **Settings** > **Branch Settings** to go to the branch settings page.
![](https://qcloudimg.tencent-cloud.cn/raw/b361241d6855a291069f4a549c0d8b24.png)
2.  Click **Add Hidden Branch**, select or enter the branch, and click **Save**. When a branch is hidden, it is shown in the hidden branch list.
3.  Use **Add User Group** or **Add Member** to specify the users that are allowed or denied access to the branch.
![](https://qcloudimg.tencent-cloud.cn/raw/82b3e9c7ad4d9a1aa6f8c3c1a9f034f9.png)

>?The priority of hidden branch access permissions is as follows: user > user group > all users. If a member belongs to multiple user groups, the member can access a hidden branch if any of their groups has access permission.
>
>For example, if User A belongs to User Group 1 (allowed access to the `dev/001` branch) and User Group 2 (denied access to the `dev/001` branch), User A can access the `dev/001` branch.
