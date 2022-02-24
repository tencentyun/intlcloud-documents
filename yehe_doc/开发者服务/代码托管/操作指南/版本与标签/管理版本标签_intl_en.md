This document describes how to manage version tags.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. Select **Code Repositories** in the menu on the left and click **Branches** to go to the branch management page.

If a multi-branch development workflow is used, we recommend you set the master branch as a [protected branch](/docs/repo/branch/protected.html). Developers can create temporary develop branches and initiate merge requests for them. After continuous integration (CI) and code reviews, developers can merge the develop branch into the master branch.



In the code repository management list, click a specific code repository to go to the details page, and then click **Versions** > **Tags** to go to the version tag management list.
![](https://qcloudimg.tencent-cloud.cn/raw/2110e9f77c2be7df683258c812a71f0c.png)
All tags in the repository are displayed in the tag list by descending order of creation time. The tag names, tag descriptions, and versions are displayed in the tag list, which also provides entries to download versions as .zip and tar.gz files and delete tags. Click a tag name or version number to go to the details page of the code version.

## Create Tag[](id:create-tag)
In the tag management list, click **Create Tag** in the upper-right corner. Enter a tag name, select the code version (branch, tag, and revision number) for the tag, and enter a tag description to create a new tag.
>?You can [Set Protected Tags](#protected-tag) on the repository settings page to standardize the tag operations of members.

![](https://qcloudimg.tencent-cloud.cn/raw/03ce7a8067e75d062cc3e9e193495759.png)

## View Release Info of a Tag[](id:view-release)
If a code version is linked to the tag, click **Version Description** to view the release details. Click **Edit Version Description** to edit the release information.
![](https://qcloudimg.tencent-cloud.cn/raw/0c75326fb1b8bd3484cdc3ac2591d75a.png)
If a tag is not linked to any release, you can click **Create Version Description** to create a release for the tag.
![](https://qcloudimg.tencent-cloud.cn/raw/25a47c8f6c79d58abf5f72faf7e5467c.png)

## Delete Tag[](id:delete-tag)
Only code tags not linked to a release can be deleted on the **Tags** page by the tag creator or admin.
![](https://qcloudimg.tencent-cloud.cn/raw/0b157f13051a86027ed72fd49e485b9c.png)

>?If a tag is associated to a release, the tag can only be deleted by deleting the linked version in **Version Release**.

## Allow Deletion and Force Push of Git Tags[](id:protected-tag)
Project admins can check the checkbox to allow deletion and force push of Git tags in **Settings** > **Code Tags**. If this is disabled, no project member can delete Git tags or force push Git tags for modification, and tags cannot be deleted on the webpage.
![](https://qcloudimg.tencent-cloud.cn/raw/a0c6d1f8de7e1d037796447210095966.png)

## Set Protected Tags[](id:protected-tag-1)
Protected tags are used to standardize the creation, update, or deletion of tags by specific members. After protected tag is enabled, only configured tag admins can create tags that match the tag rule. If `*-release` is set as a branch protection rule, non-admins will be prompted with the following when pushing the tag `xxx-release` via Git:
![](https://qcloudimg.tencent-cloud.cn/raw/7ab3ab074e38f7be30285f8d7669c31f.png)
They will also be unable to create tags or versions in Coding for Web.
![](https://qcloudimg.tencent-cloud.cn/raw/bebd00b1c3678ee391d35ba5aa8539d3.png)

#### Sample scenario

A team uses tags as triggers for CI builds. In other words, pushing tags such as v1.0-release is used as a release command in production branches.

Protected tags can be used to only allow the tag admins to create these tags for release and keep the versions organized.
