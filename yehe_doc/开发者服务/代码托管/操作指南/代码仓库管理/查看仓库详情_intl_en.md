This document describes how to view repository details.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, select **Code Repositories**.
4. If Code Repositories is not shown on the left, the project admin needs to go to **Project Settings** > **Projects and Members** > **Functions** to enable the relevant function.

On the **Code Repositories** page, click a repository name to go to the repository details page. The details page shows the files and commit history of the master branch by default.

## File List[](id:file-list)

On the repository details page, the file directory and content of the `readme` file of the master branch are shown by default.

- Click any folder in the directory on the left to list all the files in this folder in the **Files** tab on the right. You can add, rename, lock, upload, download, or delete files and folders.
![](https://qcloudimg.tencent-cloud.cn/raw/ce9a0ef4518cf605ecd49a9e855e0538.png)
- Click any file in the directory on the left to display the content of the file in the **Files** tab on the right. You can edit, rename, lock, download, or delete the selected file and view it in raw form.
![](https://qcloudimg.tencent-cloud.cn/raw/ea1e6f999258e31ac38d6143d6e1632d.png)

>? Hover over a file or folder in the directory to display the More Actions button. You can also click this button to perform the operations.

## Commit History[](id:commit-history)

1. Click the **History** tab, which shows the commit history of the master branch by default.
2. Commit records are sorted in reverse chronological order. Click the name of a commit record or the SHA ID on the right to go to the **Commits** tab for the current repository and view [Commit Details](#commit-details).
![](https://qcloudimg.tencent-cloud.cn/raw/aad2d9aab909970f57020fb60174a8d9.png)

## Commit Details[](id:commit-details)

1. On the repository details page, click **Commits** to go to the commit record management page. By default, this page lists the commit records of the master branch in reverse chronological order. You can switch to another branch to view its commit history.
![](https://qcloudimg.tencent-cloud.cn/raw/a775637f498abe2da83cf7c25004d02f.png)
2. Click the name or SHA ID of a commit record to open the details page for this record in a new tab. This page lists all the files changed in this commit.
![](https://qcloudimg.tencent-cloud.cn/raw/b91f2fe5117fb8545917fd75f4a12394.png)

>?For line-by-line code comparison, you can use [Normal Mode](#common-mode), [Side-by-Side Mode](#left-right), and [Advanced Options](#advance) to locate code differences easily. You can also comment on specific lines of code.

## Normal Mode[](id:common-mode)

In normal mode, all files changed in this commit are shown. Expand a file to see specific changes. The specific changes are displayed line by line in a file. Additions are highlighted in green and deletions are highlighted in red.
![](https://qcloudimg.tencent-cloud.cn/raw/7f41de1a677e140723b6002af7094b2c.png)

## Side-by-Side Mode[](id:left-right)

Click **Switch to Side-by-Side** to switch the code comparison mode from Normal to Side-by-Side. This mode gives you a clear view of the content before and after the changes. You can see the lines and content that have been changed. You can choose to browse the files before/after the changes or diff files.
![](https://qcloudimg.tencent-cloud.cn/raw/c9ad9e5aaeee4786055d6cb192787715.png)

## Advanced Options[](id:advance)

Advanced Options include word wrapping, show tabs, and performance mode. You can enable or disable these options as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/53cdaec60ae838e38216ba25522dd8cd.png)