This document describes how to create an SVN repository.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, select **Code Repositories**.
4. If Code Repositories is not shown on the left, the project admin needs to go to **Project Settings** > **Projects and Members** > **Functions** to enable the relevant function.

## Steps
CODING supports native SVN repositories. On the client, use SVN+SSH protocol to connect to the CODING server. All data is transmitted through SSH encrypted channels.

1.  Open a project and click **Code Repositories** on the left navigation bar to open the Code Repository Management page.
2.  In the upper-right corner of the page, click **Create Code Repository**, and then select **SVN Repository** as the repository type.
![](https://qcloudimg.tencent-cloud.cn/raw/358b2efe8c84403eb214f746b010850b.png)
3.  If you select `Create Recommended SVN Repository Layout`, the system will automatically create the `tags`, `branches`, and `trunk` directories. This is the recommended directory layout for most SVN repositories. After completing warehouse initialization, you can view SVN repository content in the Browse Code interface.
![](https://qcloudimg.tencent-cloud.cn/raw/9c589180efef74bad3dc603611ce9f15.png)
The **Browse Code** interface displays the SVN URL of the repository:
<dx-codeblock>
:::  url
svn://subversion.e.coding.net/StrayBirds/svn
:::
</dx-codeblock> 
<img src = "https://qcloudimg.tencent-cloud.cn/raw/df85f6ce1b0de892b11fe54528dad19c.png" style="width: 100%"> 
>!Currently, you must create SVN repositories in a project. You cannot create an SVN repository in a Git repository.
