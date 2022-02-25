[](id:que1)
### What is Git?
Git is a version control system. During development, version control is essential to track changes to codes, documents, and projects. However, tracking changes is far from enough to support collaboration in the modern software development field. Therefore, we need to use Git workflows to enable more efficient collaborative programming. In contrast to a centralized version control system like SVN, Git features a distributed system that offers more powerful branch management and merge capabilities. Git supports offline development and provides a solid commit process, ensuring greater development productivity for your team.

[](id:que2)
### What should I do if verification fails?
When cloning a code repository, you must enter the service email and password. You can view your service credentials by going to **Personal Account Settings** > **Personal Settings**.
![](https://qcloudimg.tencent-cloud.cn/raw/00a061fc96f20a49025dd901c6384920.png)

[](id:que3)
### What should I do if an error occurs during cloning?
1. Install and use the latest version of Git.
2. Enter `git remote -v` in the terminal to check that the associated remote URL (case sensitive) is correct:
<dx-codeblock>
:::  bash
$ git remote set-url origin https://git.coding.net:username/right-name.git
:::
</dx-codeblock>
<dx-alert infotype="explain" title="">
If the remote URL is incorrect, use the next command to modify the remote repository address.
</dx-alert>


[](id:que4)
### What should I do if another error is reported during push?
See the CODING-CR [Getting Started](https://intl.cloud.tencent.com/document/product/1132/44685) guide and make sure you have performed the operations properly. If the problem persists, send an email to <strong>support@coding.net</strong> and provide the following information so that our engineers can help solve your problem:
- Git error information.
- Result after you run git --version.
- Other useful information (such as screenshots of $ ssh -vvvT git@git.coding.net (for SSH push), $ ping coding.net, your current IP address, and your current DNS information).

[](id:que5)
### What should I do if the prompt "couldn't resolve host" appears?
This may be due to your DNS settings. Change your DNS to 114.114.114.114 or 1.1.1.1 and try again.

[](id:que6)
### What should I do if the prompt "permission denied (publickey)" appears?
This may occur when you do not have permission for the target repository or branch, so you cannot update data.
- Verify your push method. If you are using SSH, check that your SSH public key is correct (if you have multiple private keys, use ssh-add to specify the default private key).
- If you are using HTTPS, check that the username and password are correct.
- Make sure you have the write permission for the target branch.

[](id:que7)
### Do sub-users have permission to access CODING DevOps?
As long as the root account has access to CODING DevOps, its sub-users can directly access CODING DevOps. To see if sub-users have access, check that the roles and policies of the root account meet the following access requirements:
The CODING_QCSRole role and QcloudAccessForCODINGRole policy are both present.
- If the CODING_QCSRole role is missing, log in to the [CODING DevOps Console](https://console.cloud.tencent.com/coding) with the root account, click the Team Space link, and complete authorization as instructed.
- If the root account is missing the QcloudAccessForCODINGRole policy, log in to the [Access Management Console](https://console.cloud.tencent.com/cam/overview) with the root account and go to **Roles** > **CODING_QCSRole** to add the QcloudAccessForCODINGRole policy.
