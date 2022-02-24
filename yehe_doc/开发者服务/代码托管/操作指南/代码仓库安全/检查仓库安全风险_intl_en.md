This document describes how to check for security risks in a code repository.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, click **Code Repositories** > **Settings** to go to the repository security page.

Project admins can view existing security risks in **Settings** > **Repository Security**.
![](https://qcloudimg.tencent-cloud.cn/raw/cd0d131f32b5ee90c3e7b4de4ff5a6a2.png)

The following checks on code repositories are available:

-   Whether the check of the Git committer and author is enabled.
-   Whether a GPG public key has been uploaded.
-   Whether a protected branch has been set. Whether branch admins have been set and review by the code owner has been enabled for protected branches.

>?To keep your repository secure, we recommend you configure the relevant features with reference to [Push Settings](https://intl.cloud.tencent.com/document/product/1132/44726), [Using GPG to Sign Commit Records](https://intl.cloud.tencent.com/document/product/1132/44725), and [Protected Branch](https://intl.cloud.tencent.com/document/product/1132/44715).
