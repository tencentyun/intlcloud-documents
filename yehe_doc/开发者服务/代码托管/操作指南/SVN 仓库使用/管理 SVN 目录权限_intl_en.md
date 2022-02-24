This document describes how to manage SVN repository permissions.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, select **Code Repositories**.
4. If Code Repositories is not shown on the left, the project admin needs to go to **Project Settings** > **Projects and Members** > **Functions** to enable the relevant function.

SVN code repositories support permission control. Admins can set directory permissions for individual users. Admins can set three types of permissions for repositories and subdirectories:

-   **Read-only**: Users can check out and view the specified directory, but cannot write to it.
-   **Read/Write**: Users can check out, view, and write to the specified directory.
-   **No permission**: Users cannot check out, view, or write to the specified directory.

## Set Permissions[](id:set-permission)

1. Because each user has read/write permission for a repository by default, to set permission control for a directory in an SVN repository, you must click the More button for the directory and select **Permissions**.
![](https://qcloudimg.tencent-cloud.cn/raw/8e1dcfb3306ca8089622ea146a023d7c.png)
2. On the permission settings page that appears, you can add individual users and corresponding permissions for this directory.
![](https://qcloudimg.tencent-cloud.cn/raw/5d2fbd8d65101655f4727699253cdff6.png)
3. After you configure permission control for a directory, the directory is shown in a different color. Directories for which you have not configured permission control are shown in black, and all users have **read/write** permission for this directory.
 -   **Read/Write**: black (default)
 -   **Read-only**: yellow
 -   **No permission**: gray
![](https://qcloudimg.tencent-cloud.cn/raw/d91e475ca50385cd85d861fb50741a25.png)

## Permission Precedence[](id:overwrite)

In some scenarios, different permission settings may be configured for a parent directory and its subdirectories. For example, a user may have read-only permission for the parent directory and read/write permission for a subdirectory. For an SVN repository, the precedence rules for parent directory permissions and subdirectory permissions are as follows:

-   If permissions are set for the parent directory but not its subdirectory, the subdirectory inherits the permission settings of the parent directory.
-   If permissions are set for both the parent directory and subdirectory, the subdirectory permissions take precedence. For example:
    1.  If there is **read/write** permission to the parent directory and **read-only** permission to the subdirectory, the effective permission for the subdirectory is **read-only**.
    2.  If there is **read-only** permission to the parent directory and **read/write** permission to the subdirectory, the effective permission for the subdirectory is **read/write**. 
    3.  If there is **read/write** or **read-only** permission to the parent directory and there is **no permission** to the subdirectory, the effective permission for the subdirectory is **no permission**.
