This document describes how to use SSH protocol to push/pull code.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, select **Code Repositories**.
4. If Code Repositories is not shown on the left, the project admin needs to go to **Project Settings** > **Projects and Members** > **Functions** to enable the relevant function.

CODING supports pushing/pulling code via SSH protocol.

1.  Refer to [Configure Public Keys](https://intl.cloud.tencent.com/document/product/1132/44710) to generate a public key and add it to a code repository or personal account.
2.  Copy the SSH URL on the code repository's Browse page.
![](https://qcloudimg.tencent-cloud.cn/raw/b2a969922ec6f66d52976e0b1991751b.png)
3.  Run the `git clone + repository URL` command on your local machine to pull code.
![](https://qcloudimg.tencent-cloud.cn/raw/c0e70032484c55eeb4bf4c4dc0fbd638.png)
