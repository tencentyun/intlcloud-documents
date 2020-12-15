## Overview
Before using a Git repository to build container images, you need to authorize TKE to access the code source. Currently, TKE supports GitHub repository and GitLab repository.



## Prerequisites
You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2).

## Directions
### Selecting a code source
1. Choose **Image Repository** > **[My Images](https://console.cloud.tencent.com/tke2/registry/user)** in the left sidebar.
2. On the **My Images** page, click **Source Authorization**, as shown in the following figure.
>?”Source Authorization” is only available in China mainland, namely the “Default Region” on the console.

![](https://main.qcloudimg.com/raw/8706fe2e04fbc6ca92f6a16e8b9156b7.png)
3. In the **Code Source Authorization** window that appears, select an option as needed, as shown in the following figure.
>!A user can authorize both GitHub and GitLab accounts at the same time, but only one account of each type. To change your bound GitHub or GitLab account, you need to unbind the original account.

![](https://main.qcloudimg.com/raw/4347572f30004d7ecb60bd67d23fe290.png)
 - If your repository is on GitHub, see [Authorizing GitHub](#Github) to complete the authorization.
 - If your repository is on an on-premises GitLab server or a GitLab managed server, see [Authorizing GitLab](#Gitlab) to complete the authorization.

<span id="Github"></span>
### Github authorization
1. In the **Code Source Authorization** window, click **Authorize to sync Github code source**.
2. For the first time of authorization, you will be directed to the GitHub website and see a prompt stating that the app needs to access your repositories and personal data, as shown in the following figure.
![](https://main.qcloudimg.com/raw/649cab61cc2a4a603775bbf3524b1731.png)
3. Click **Authorize** to finish authorizing a GitHub repository, as shown in the following figure.
![](https://main.qcloudimg.com/raw/db0b50852c44f13330fe3268f1bd0081.png)

<span id="Gitlab"></span>
### Gitlab authorization

<span ID="AccessToken"></span>
#### Obtaining the Access Token of GitLab
1. Log in to the [GitLab website](https://gitlab.com) and go to the **Create Access Token** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/442fff57fd7f25b6b92d24b42108f6c7.png)
  1. Click your profile photo. In the drop-down menu, select **Settings**.
  2. In the left pane of the "User Settings" page, click **Access Tokens** to go to the **Create Access Token** page.
On the “Create Access Token" page, set the following information as needed:
![](https://main.qcloudimg.com/raw/8c5d26f5db15e23858f09c237d0a9a00.png)
 - **Name**: enter a name for the new access token.
 - **Expires at**: set the expiration date of the new access token.
 - **Scopes**: set the access scope of the new access token. **The API option is required**.
 >!
 >- The API option is required for Scopes. Otherwise, you will not be able to obtain source repository information or set callback hooks for auto building.
 >- Set a reasonable expiration date for the token to ensure that it is always valid during usage.
3. Click **Create** and save the created access token, as shown in the following figure.
![](https://main.qcloudimg.com/raw/750311050a69d7ff70bc72e6678246e7.png)


#### Authorizing GitLab code source synchronization
1. In the **Code Source Authorization** window, click **Authorize to sync GitLab code source** and enter the following information:
![](https://main.qcloudimg.com/raw/e38a3b29d30c1e604437e72bb2df8148.png)
 - **Service address**: indicates the URL of the GitLab server, which must use the HTTP or HTTPS protocol and can be accessed over the public network. For example, `https://you-gitlab.com`. Do not enter the URL of a specific project or repository.
 - **Private token**: must be the Access Token. If you do not have the Access Token yet, see [Obtaining a GitLab access token](#AccessToken) and create one.
2. Click **OK** to finish the authorization, as shown in the following figure.
![](https://main.qcloudimg.com/raw/7689221c9f26028c56df0e676a601eac.png)


