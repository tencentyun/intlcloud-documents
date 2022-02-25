This document describes how to create branches in code repositories.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. Select **Code Repositories** in the menu on the left and click **Branches** to go to the branch management page.

Branches are a common function in Git. The common development approach is to retain one trunk (or master branch), while each development or bug fix task is carried out on its own branch. When finished, the branches are merged back into the trunk. Because development directly on the trunk is very risky, the branch can be viewed as a safety valve, which isolates different development tasks. It can ensure that the stability of the master version is not compromised, while allowing different people to focus on different development tasks.

>? Below, we will refer to branches in CODING code repositories as remote branches and branches in local Git repositories as local branches. You can run commands on your local terminal to quickly create branches. For details, see [Common Git Commands](https://intl.cloud.tencent.com/document/product/1132/44728).


1.  Go to the code repository details page and click the **Branches** tab to see all branches in the remote repository.
Here, you can create branches and enable protected branches. The branch list tab displays the number of additional or missing commits relative to the default branch at present.
![](https://qcloudimg.tencent-cloud.cn/raw/aa8ce1c4f59ea3a817bbd97abb31cf5c.png)

2.  Click **Create Branch** in the upper-right corner and follow the instructions in the pop-up window to enter the relevant configuration information. The master branch is used as the source by default, and a new branch is derived from this source.
![](https://qcloudimg.tencent-cloud.cn/raw/9be7bb457f610655656b6f4e9a52fa98.png)
3.  When creating a branch, you can add a simple description to indicate the purpose of the branch. When the branch name cannot fully indicate its purpose, add additional information in the Branch Note.
![](https://qcloudimg.tencent-cloud.cn/raw/706da2fbaa39fc783d0e3c9e995c6794.png)
