This document describes how to use key fingerprints for code repository authentication. This ensures that the connected remote repository is a genuine CODING repository.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, select **Code Repositories**.
4. If Code Repositories is not shown on the left, the project admin needs to go to **Project Settings** > **Projects and Members** > **Functions** to enable the relevant function.

## Function Overview[](id:intro)

Code security is always essential. To ensure that the remote repository you are connecting to is an authentic CODING code repository, SSH key fingerprints are now provided for authentication. You simply need to run the command locally and verify the returned result to determine the authenticity of the remote repository.

## Verify SHA256 Fingerprint[](id:sha256)

View the `e.coding.net` SHA256 fingerprint in the local `.ssh/know_hosts` file. If the return value is `jok3FH7q5LJ6qvE7iPNehBgXRw51ErE77S0Dn+Vg/Ik`, this indicates you have connected to the correct CODING server. You can view the result of the command on the terminal.
<dx-codeblock>
:::  bash
ssh-keygen -lf ~/.ssh/known_hosts
:::
</dx-codeblock>

![](https://qcloudimg.tencent-cloud.cn/raw/13301b96bbccb08ebc1d78f23858ea96.png)

## Verify MD5 Fingerprint[](id:md5)

View the `e.coding.net` MD5 fingerprint in the local `.ssh/know_hosts` file. If the return value is `98:ab:2b:30:60:00:82:86:bb:85:db:87:22:c4:4f:b1`, this indicates you have connected to the correct CODING server. You can view the result of the command on the terminal.
<dx-codeblock>
:::  bash
ssh-keygen -E md5 -lf ~/.ssh/known_hosts
:::
</dx-codeblock>

![](https://qcloudimg.tencent-cloud.cn/raw/409314f22ce3b4d3f0cb423ffc1527a8.png)
