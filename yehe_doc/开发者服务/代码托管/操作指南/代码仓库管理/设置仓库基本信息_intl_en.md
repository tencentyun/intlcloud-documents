This document describes how to set basic repository information.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, select **Code Repositories**.
4. If Code Repositories is not shown on the left, the project admin needs to go to **Project Settings** > **Projects and Members** > **Functions** to enable the relevant function.


## Steps
1. Open a project, go to the **Code Repositories** module, and click a repository to go to its details page. In the **Settings** tab, you can configure the settings of the current repository.
>? Only project admins can access the Settings page of a repository.
>
![](https://qcloudimg.tencent-cloud.cn/raw/fb07986d7e12258c411c4a281d47a369.png)
2. On the **Basic Settings** page, you can modify the name and icon of your repository. Changing the repository name will change its access URL, so the previous URL will no longer work. After you change the name, you must match the new URL in your local repository.
```bash
git remote set-url origin https://e.coding.net/codingcorp/coding-help-generator/[new-repo-name].git
```
In addition, you can add a repository description and view the code repository capacity on this page. If necessary, you can archive, reset, or delete the repository.
