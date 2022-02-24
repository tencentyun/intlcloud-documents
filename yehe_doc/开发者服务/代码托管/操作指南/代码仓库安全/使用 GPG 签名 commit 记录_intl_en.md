This document describes how to sign commits with GPG.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.

CODING allows you to use GPG for Git commit signature verification. Verified commits will be tagged with **Verified**, which ensures that code is committed from reliable sources and enhances code security.

To sign Git commits with GPG:
<dx-steps>
-Step 1: [Generate a GPG key pair](#generate)
-Step 2: [Add a GPG public key in your personal account settings](#upload)
-Step 3: [Associate with the local Git repository](#associate)
-Step 4: [Sign Git commits](#sign)
-Step 5: [Verify signatures](#verify)
</dx-steps>


## Step 1: Generate a GPG Key Pair[](id:generate)

1.  [Download](https://www.gnupg.org/download/index.html) and install GPG. If you are using macOS, use the brew package management tool to run the following command:
<dx-codeblock>
:::  shell
brew install gpg  
:::
</dx-codeblock>
2.  Run the following command to generate a GPG key pair (public key/private key):
<dx-codeblock>
:::  shell
gpg --full-gen-key  
:::
</dx-codeblock>
<dx-alert infotype="explain" title="">
In certain scenarios, such as if you are using Windows Gpg4win or other macOS versions, use the `gpg --gen-key` command to generate a key pair.
</dx-alert> 
As the command is interactive, you need to specify the algorithm, validity period, your real name and email address, a password, etc.<ul>
 <li><b>Key type</b>: Select the key type or press <code>Enter</code> to select the default type (RSA and RSA).</li>
 <li><b>Elliptic curve</b>: Press <code>Enter</code> to select the default <code>Curve 25519</code>.</li>
 <li><b>Validity</b>: Specify the validity period of the key as needed or press <code>Enter</code> to select the default `Never expire`.</li>
 <li><b>Email address</b>: Enter the email address configured in your CODING account.</li></ul>
3.  Run the following command to list the GPG key you just created (replace "your_email" with the email address entered in Step 3):
<dx-codeblock>
:::  shell
gpg --list-secret-keys --keyid-format LONG "your_email" 
:::
</dx-codeblock>
4.  Copy the GPG key ID that starts with `sec`. In the following example, copy `4AEA00A342C24CA3`:
<dx-codeblock>
:::  shell
sec   ed25519/4AEA00A342C24CA3 2021-09-14 [SC]
      6DE3507E82DEB6E8828FAAC34AEA00A342C24BD4
uid                 [ ultimate ] your_name "your_email"
ssb   cv25519/812B586FD245B560 2021-09-14 [E]
:::
</dx-codeblock>
5.  Export the public key of that ID  (using the above ID as an example):
<dx-codeblock>
:::  shell
gpg --armor --export 4AEA00A342C24CA3
:::
</dx-codeblock>
6.  After the public key is generated, [add it to your CODING account](#upload).

## Step 2: Add a Public Key in Your Personal Account Settings[](id:upload)

1.  After you have logged in to CODING, click your profile photo in the upper-right corner and select **Personal Account Settings**.
2.  In the navigation bar on the left, select **GPG Public Key** to go to the public key management page.
3.  Click **Add Public Key** and paste the exported GPG public key in the text box, and then click OK.
![](https://qcloudimg.tencent-cloud.cn/raw/b416d8381345043661d0d284799a92c4.png)
After the public key is added, the verification status of the email address, key ID, and subkey will be shown.
![](https://qcloudimg.tencent-cloud.cn/raw/5de6ba83223227468315c1b07b40a94c.png)

>?If the status of the email address is Not Verified, the email address is not configured in the CODING account. Add the email address in **Personal Account Settings** > **Email Settings**.

## Step 3: Associate with the Local Git Repository[](id:associate)

1.  Run the following command to list the GPG key you created (replace "your_email" with the email address entered when generating the key):
<dx-codeblock>
:::  shell
gpg --list-secret-keys --keyid-format LONG "your_email"
:::
</dx-codeblock>
2.  Copy the GPG key ID that starts with `sec`. In the following example, copy `4AEA00A342C24CA3`:
<dx-codeblock>
:::  shell
sec   ed25519/4AEA00A342C24CA3 2021-09-14 [SC]
      6DE3507E82DEB6E8828FAAC34AEA00A342C24BD4
uid                 [ ultimate ] your_name "your_email"
ssb   cv25519/812B586FD245B560 2021-09-14 [E]
:::
</dx-codeblock>
3.  Configure the key in the local Git repository to sign the commits with it:
<dx-codeblock>
:::  shell
git config --global user.signingkey 4AEA00A342C24CA3
:::
</dx-codeblock>
You have now successfully associated the GPG key with the local Git repository. After modifying code locally, you can sign your Git commits to verify the committer.

## Step 4: Sign Git Commits[](id:sign)

Use the `-S` parameter when running a Git commit command.

1.  When you need to commit changes after editing code locally, add the `-S` parameter to the `git commit` command:
<dx-codeblock>
:::  shell
git commit -S -m "your_commit_message"
:::
</dx-codeblock>
If you do not wish to enter the `-S` flag every time, you can use the following command to allow Git to sign commits automatically:
<dx-codeblock>
:::  shell
git config --global commit.gpgsign true
:::
</dx-codeblock>
2.  When asked, enter the password specified when generating the GPG key.

## Step 5: Verify Signature[](id:verify)

After pushing the signed commit to the CODING code repository, you can check the verification status of the commit on the **Commits** tab in the code repository.
![](https://qcloudimg.tencent-cloud.cn/raw/32b6400f1c20a6732ccbfd236a3e3c7a.png)

Commit verification statuses are described below:

|Verification Status|Description|
|:------|:---|
|Verified	|Signed with a GPG private key that corresponds to a public key in a CODING account, and the email address for the public key has been verified.|
|Not Verified	|Signed with a GPG private key that does not correspond to a public key in a CODING account or the email address for the public key has not been verified<br>(if the email address is Not Verified, go to **Personal Account Settings** > **Email Settings** to add the email address). |
|No verification status tag	|Not signed with a GPG private key|

## Delete a GPG Public Key[](id:delete)

If your GPG public key has been compromised or is no longer used, you can delete the public key in **Personal Account Settings** > **GPG Public Key**.
![](https://qcloudimg.tencent-cloud.cn/raw/b91fd2a8526828dc2ea2f9d88f1698c3.png)

After the public key is deleted:

-   Verified commits will change to a Not Verified status.
-   Future commits using this GPG private key (`git commit -S -m`) will stay unverified.
-   Unsigned commits (`git commit -m`) will not be verified and will not have a verification status tag.

![](https://qcloudimg.tencent-cloud.cn/raw/f227308d27e4a0db11d343238706e306.png)

>?If you have enabled Git automatic signing, run the `git config --global commit.gpgsign false` command to disable automatic signing. Otherwise, commits pushed to the remote repository will still be **Not Verified** after the GPG public key is deleted.


## Fix GPG Signing Errors[](id:delete)

If the following error occurs when using `git commit -S -m`, see [Fix GPG Signing Errors](https://www.wevg.org/archives/fix-gpg-sign-error/) and modify the relevant configurations.
<dx-codeblock>
:::  txt
error: gpg failed to sign the data
fatal: failed to write commit object
:::
</dx-codeblock>

