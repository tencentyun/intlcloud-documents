In CODING, SSH public keys have different permission scopes depending on the usage scenario. This document describes the differences between SSH public keys and project tokens.

## Function Overview[](id:intro)

SSH public key files associated with a CODING account are referred to as **SSH Public Keys**. After they are configured, they have read and write permissions to all projects. If they are associated with a certain project, they are referred to as **Project Tokens**. After they are configured, they have read-only permission to the project by default.

## Generate a Public Key[](id:generate)

Run the following commands:
<dx-codeblock>
:::  shell
ssh-keygen -m PEM -t rsa -b 4096 -C "your.email@example.com"
# Creates a new ssh key, using the provided email as a label
# Generating public/private rsa key pair.
Enter file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]  // We recommend using the default address
Enter passphrase (empty for no passphrase):   // Press Enter without entering a passphrase. If you enter one, you will need to enter the passphrase every time you push code using SSH.
:::
</dx-codeblock>

If you need multiple SSH key pairs (you may be working with multiple code hosting platforms), when you are prompted to "Enter file in which to save the key", enter a new file name, so the default key pair will not be overwritten.

After the operation succeeds, you will see the following information:
<dx-codeblock>
:::  shell
Your identification has been saved in /Users/you/.ssh/id_rsa.
# Your public key has been saved in /Users/you/.ssh/id_rsa.pub.
# The key fingerprint is:
# 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your.email@example.com
:::
</dx-codeblock>


## Add the SSH Public Key[](id:account-ssh)

1.  Enter "open ~/.ssh" in the terminal, open the "id_rsa.pub" file with a text editor, and copy all the content. (id_rsa.pub is the default name of the generated public key. Open the corresponding file if you used a different name.)
2.  Click your profile photo in the upper-right corner of the page and select **Personal Account Settings**. Go to **Personal Account Settings** > **Personal Settings** > **SSH Public Keys**.
![](https://qcloudimg.tencent-cloud.cn/raw/35540a469ad9d8ef6ba6fb8e79bf49e5.png)
3.  Paste the content copied in Step 1 into the **Public Key** field and enter a key name.
4.  Set the validity of the public key. You can select a specific expiration date or set it to Never expire.
![](https://qcloudimg.tencent-cloud.cn/raw/396f688414ace2681660ec9959d5605f.png)
5.  Click **Add** and enter the password to add the public key.
6.  Then, run a test in the command line. You will need to trust the host when establishing a connection for the first time. Run the `ssh -T git@e.coding.net` command. You can also verify whether the connection with a CODING remote repository is correct using [Key Fingerprint Authentication](/docs/repo/ssh/fingerprint.html).

## Add the Public Deploy Key[](id:project-ssh)

1.  Enter "open ~/.ssh" in the terminal, open the "id_deploy.pub" file with a text editor, and copy all the content. (The public deploy key here is named "id_deploy.pub". You can customize the name when generating the public deploy key.)
2.  In the target project, go to the code repository > **Public Deploy Key** and click **Create Public Deploy Key**.
![](https://qcloudimg.tencent-cloud.cn/raw/6669895c2e6c1b8fcfbe262049161b07.png)
3.  Paste the content copied in Step 1 into the **Public Key** field and enter a key name.
4.  Click **Create** and enter the password to add the public deploy key.

>?Public deploy keys have read-only permission to the project by default. Select **Grant Push Permission** to obtain push permission.
