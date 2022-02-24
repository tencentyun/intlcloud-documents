This document describes how to use the version release feature in a code repository.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, click **Code Repositories** > **Versions** to go to the version page.

In the code repository management list, click a specific code repository and go to the details page, and then click **Versions** > **Version Release** to go to the version release list.
![](https://qcloudimg.tencent-cloud.cn/raw/6e4a4e20a3673482690d84ed0e140bcc.png)

The version release list displays code versions released in a project with their tag names and committed versions by descending order of creation time.


## Create Code Version[](id:create-version)

1.  On the version management page, click the Create Code Version button in the upper-right corner.
>?You can [set the default release branch](#delete-tag) on the repository settings page.
2.  Enter a tag version, release title, and version description. You can upload files smaller than 100 MB and associate resources in the project (such as tasks, files, Wiki pages, and merge requests). Only new tag names are allowed and you need to select a source for new tag versions (branch, tag, or revision number).
![](https://qcloudimg.tencent-cloud.cn/raw/70aa1c82152b71d8dfb11d836e0fc45e.png)
3.  After entering the above information, you can mark the version as a pre-release, and then create the code release. After the code version is created, the version list will be similar to the following image. The latest release is the latest official version release.
![](https://qcloudimg.tencent-cloud.cn/raw/6e4a4e20a3673482690d84ed0e140bcc.png)

## Edit Code Version[](id:edit-version)

Click any code version in the version release list and go to the details page. The release creator or project admins can click the Edit Version Description button to edit all information except the tag name.
![](https://qcloudimg.tencent-cloud.cn/raw/4161d5a3baf886d1b4824c2b2997b4e0.png)

## Delete Code Version[](id:delete-version)

On the details page of a code version, the release creator or project admins can delete the version by clicking on the Delete icon.

>?You can also delete the linked version tags when deleting a version. You can only use or create a tag with the same name after you have deleted the version tag.
>
![](https://qcloudimg.tencent-cloud.cn/raw/0cb22e263ee2dbf7fbe9460e491cca8d.png)

## Set the Default Release Branch[](id:delete-tag)

Project admins can specify the default branch for version releases in **Settings** > **Version Release**.
![](https://qcloudimg.tencent-cloud.cn/raw/de1fd6cc14c3ca33bab9d6a65fa6e45e.png)
