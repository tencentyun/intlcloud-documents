This document describes how to create repositories.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, select **Code Repositories**.
4. If Code Repositories is not shown on the left, the project admin needs to go to **Project Settings** > **Projects and Members** > **Functions** to enable the relevant function.

## Create Git and SVN Repositories[](id:common-create)

### Create a Git repository[](id:git)

1.  In the code repository list, click **Create Code Repository** in the top-right corner and select **Create from Scratch**.
2.  Select Git as the repository type and enter a valid repository name.
3.  We recommend you select the **Generate README File** option. When this is enabled, the Git repository is automatically initialized after creation.
4.  We recommend you select **Private Repository**. Enable the **Code Scanning** function as needed to discover and avoid potential code issues.
5.  Click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/bb755ddf5fc74db3a350eaf137820a54.png)

>?After the repository is initialized, you can use Git commands to associate it when a local repository. For details, see [Common Git Commands](https://intl.cloud.tencent.com/document/product/1132/44728).

### Create an SVN repository[](id:svn)

CODING supports the creation of SVN repositories. For more information about creating and using SVN repositories, see [SVN Repository Usage](https://intl.cloud.tencent.com/document/product/1132/44707).

## Create from Template[](id:template-create)

CODING provides a preset code repository module. You can use sample code to learn how the code repository module works with continuous integration and artifacts.
![](https://qcloudimg.tencent-cloud.cn/raw/59ecf65114c0a7aa1fed885614896423.png)

## Import an External Repository[](id:import-create)

You can quickly migrate existing Git repositories to the CODING DevOps platform. For details, see [Import or Associate External Repository](https://intl.cloud.tencent.com/document/product/1132/44699).
