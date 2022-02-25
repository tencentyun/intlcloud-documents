## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, select **Code Repositories**.
4. If Code Repositories is not shown on the left, the project admin needs to go to **Project Settings** > **Projects and Members** > **Functions** to enable the relevant function.


## Import External Code Repositories
CODING-CR provides a quick import function for external open-source repositories and allows you to sync code with external repositories at regular intervals. When creating a code repository, select **Import External Repository** and enter the URL of the open-source Git repository to import.
![](https://qcloudimg.tencent-cloud.cn/raw/62c046eabd9294be95173267bc0759e8.png)
You can sync the repository with the source repository and the changes made in CODING will be overwritten. You can change the sync frequency or disable auto sync in the repository settings.
![](https://qcloudimg.tencent-cloud.cn/raw/cf0ecc319dd9d88052f696d757e4efde.png)

## Associate a Code Repository
The **Associate Repository** function allows you to temporarily store the credentials used to access an external repository in CODING. When using **Continuous Integration** or **Continuous Deployment**, you can directly use the third-party repository as a code source without repeated migration.
![](https://qcloudimg.tencent-cloud.cn/raw/ad06aad9452ca85e7c2d08c47560581d.png)
GitHub, GitLab, private GitLab, Gitee, TGit, and common Git repositories can be associated with CODING repositories. These five repository types support OAuth verification. Common Git repositories support account password verification. After association, repository code will not be stored in the CODING repository.
![](https://qcloudimg.tencent-cloud.cn/raw/3f3db45dceff06f2dbad545dc4f7ed32.png)

### Associate a private GitLab repository
To associate a private GitLab repository, you must create an application in GitLab and then the team admin must bind the private GitLab service. For details, see [Bind Private GitLab](https://help.coding.net/docs/admin/service-integration/gitlab.html).


### Associate a GitLab SaaS repository
To associate a GitLab SaaS repository, Select **GitLab** as the code source on the **Associate Code Repository** page. Then, click **Verify Now** to go to the GitLab Authorization page and click **Authorize** to complete authorization. After successful authorization, select the code repository to associate.


### Associate a GitHub repository
On the **Associate Code Repository** page, select the **GitHub** code source and click **Verify Now** to go to GitHub for OAuth authorization. If authorization fails, this may be because you did not enter your username in GitHub. In this case, go to **Settings** > **Profile** > **Name** and enter your username.