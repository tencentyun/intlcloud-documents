This document describes how to configure SSH public keys.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, select **Code Repositories**.
4. If Code Repositories is not shown on the left, the project admin needs to go to **Project Settings** > **Projects and Members** > **Functions** to enable the relevant function.

## Function Overview[](id:intro)

SSH stands for Secure Shell. It is an encryption protocol used for network communication. SSH provides a secure data transmission environment in a public network environment. It is generally used to log in to a remote host and push/pull code.

You can add an SSH public key to a code repository, where it is called a **public deploy key**. Then, this key will grant read-only permission for this project by default. If you add the key to a personal account, it is called an **SSH public key**. It grants read/write permission to all projects under the account. The same SSH public key cannot be added to code repositories or personal accounts more than once.

## Generate Public Key[](id:keygen)

Here, we use the `ssh-keygen` tool to generate an SSH public key. Run the following command:
<dx-codeblock>
:::  shell
ssh-keygen -m PEM -t rsa -b 4096 -C "your.email@example.com"  // Creates a new SSH key pair (public key/private key). Enter your email as the tag.
Enter file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]  // We recommend using the default address
Enter passphrase (empty for no passphrase):  // Here, just press Enter. If you set a passphrase, you will need to enter the passphrase every time you push code using SSH.
:::
</dx-codeblock>

>? If you need multiple SSH key pairs, when you are prompted to `Enter file in which to save the key`, enter a new file name, so the existing key pair will not be overwritten. For more information about SSH, see [Wikipedia](http://zh.wikipedia.org/zh/Secure_Shell).

After the operation succeeds, you will see the following information:
<dx-codeblock>
:::  shell
Your identification has been saved in /Users/you/.ssh/id_rsa.
# Your public key has been saved in /Users/you/.ssh/id_rsa.pub.
# The key fingerprint is:
# 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your.email@example.com
:::
</dx-codeblock>


## Add Public Key[](id:add-key)

You can add a public key to a code repository or personal account.

### Associate public key with code repository[](id:deploy-key)

1.  Go to the key pair address generated above (generally `~/.ssh/`) and find the public key file with the `pub` extension. Use the `cat` command to output all content and copy the content.
![](https://qcloudimg.tencent-cloud.cn/raw/676a223b47469c71a4d49e4494028d95.png)
2.  Open the code repository and go to **Settings** > **Public Deploy Key**. Click **Add Public Deploy Key** and paste the full text of the public key.
![](https://qcloudimg.tencent-cloud.cn/raw/98aa7f3477b4f2de0cbb6ad86d480e38.png)
>? Public deploy keys have read-only permission to the project by default. Select **Grant Push Permission** in the public deploy key settings to obtain push permission.
>
3.  Then, the first time you attempt to connect from your local device, run the public key authentication command: `ssh -T git@e.coding.net`
![](https://qcloudimg.tencent-cloud.cn/raw/2c8f0745c6ed72f3eddf6867f1e6287e.png)

### Associate public key with personal account[](id:account-key)

1.  Go to the key pair address generated above (the default address is generally `~/.ssh/`) and find the public key file with the `pub` extension. Use the `cat` command to output all content and copy the content.
![](https://qcloudimg.tencent-cloud.cn/raw/00ddfcf7b9f82b8569dad32aaf7dd7d7.png)
2.  Log in to CODING, click your profile photo in the upper-right corner, and go to **Personal Account Settings** > **SSH Public Keys**. Then, click **Create Public Key**.
![](https://qcloudimg.tencent-cloud.cn/raw/ecb4edf702018c455ba79fb0dd145316.png)
3.  Follow the instructions to paste the public key content you copied and enter a name for the public key.
4.  Then, the first time you attempt to connect from your local device, run the public key authentication command: `ssh -T git@e.coding.net`.
![](https://qcloudimg.tencent-cloud.cn/raw/2c8f0745c6ed72f3eddf6867f1e6287e.png)
