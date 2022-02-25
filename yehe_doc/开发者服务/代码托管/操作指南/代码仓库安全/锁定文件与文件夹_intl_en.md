This document describes how to lock files and folders in a code repository.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.

CODING allows you to lock files or paths of the **Default Branch (usually the master branch)** in code repositories. Only the user who locked the file can modify (edit or delete) it. If a user locks a path, all files in the path will be locked and can only be modified by the user who locked it.

## Permission Description[](id:permission)

Project admins can enter the project, click **Project Settings** in the lower-left corner, and go to **Projects and Members** > **User Groups** to set permissions for the repository. After setting the permissions, add team members to the relevant user groups to control the permissions to code repositories in the project.
![](https://qcloudimg.tencent-cloud.cn/raw/442b4641142679a150d28c97ce65b58f.png)

-   A project member with permission to **Access Code Repositories** can lock files or paths on the Browse page. Locked files or paths can be unlocked on the Browse page.
-   A user can only unlock files or paths they locked; a member with permission to **Unlock Locked Files** can unlock files or paths locked by another user.

## Lock a File[](id:lock-file)

Go to the Browse page of a project repository and select a file. Click the More Actions button in the upper-right corner and select Lock.
![](https://qcloudimg.tencent-cloud.cn/raw/b9470ab4e8ae43cf8c079af3cf741a97.png)
 A padlock icon will appear after the file is locked. Only the member who locked this file can edit or delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/93b5c5a053be0a2cdb1358e976e735d0.png)

## Lock a Folder[](id:lock-path)

Select a folder in a repository, click the More Actions button in the upper-right corner, and then select Lock to lock all files in the path.
![](https://qcloudimg.tencent-cloud.cn/raw/717cffad0967754a1267718ef7f914b2.png)

## Lock Result[](id:result)

A locked file can only be edited/deleted by the user who locked the file. Only the user who locked the path can create/edit/delete files in it. If another user tries to modify the locked file by pushing, the push will fail.
![](https://qcloudimg.tencent-cloud.cn/raw/0496468fbfc1909bb427ce8b2f526e81.png)

In a merge request, if the target branch is the default branch and the directory to be written includes a locked file or path, the merge can only be performed by the user who locked the file or path. Other members cannot merge the branches.
![](https://qcloudimg.tencent-cloud.cn/raw/7b2072035a6f0180c150a63e6d529538.png)

## Unlock a Locked File or Folder[](id:view-lock-file)

A project member can unlock files or folders they locked on the Browse page; a member with permission to **Unlock Locked Files** can unlock files or folders locked by another user.
![](https://qcloudimg.tencent-cloud.cn/raw/d960ea74528f171c3716fd21f04b167b.png)

Project admins can view locked files/folders in **Settings** > **File Locking**. Click **Delete** to unlock the file or folder.
![](https://qcloudimg.tencent-cloud.cn/raw/4a2b556c38fed82dcacb47bf73524de9.png)
