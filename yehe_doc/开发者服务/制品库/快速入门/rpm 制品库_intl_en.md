This document describes how to store RPM artifacts in CODING-AR for centralized artifact management and version control. The following sections introduce how to create an artifact, configure authentication, and pull and push artifacts.

## Open CODING-AR

1. Log in to the CODING Console and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Artifact Management**.

## Preparations

>! Before you begin:
> -  Prepare a Linux environment.
> -   Create an artifact repository (see [Basic Operations](https://intl.cloud.tencent.com/document/product/1136/44804)).
> -   Select RPM as the repository type.

## Initialize a Local RPM Project[](#init)

RPM is installed in Linux by default. You can run rpm commands in a Linux terminal directly. To use rpm commands in other operating systems, use Docker to install CentOS:
<dx-codeblock>
:::  bash
docker run -it --name centos centos:8 /bin/bash
:::
</dx-codeblock>


## Download a Demo Project[](#download)

Visit the [RPM artifact website](https://www.rpmfind.net/) to search for an artifact and download and install it.

For example:
<dx-codeblock>
:::  bash
wget -N --no-check-certificate "https://www.rpmfind.net/linux/fedora/linux/development/rawhide/Everything/aarch64/os/Packages/h/hello-2.10-5.fc34.aarch64.rpm" && rpm -i hello-2.10-5.fc34.aarch64.rpm
:::
</dx-codeblock>

## Configure Authentication Information[](#config)

Click **Generate configuration from access token** in "Guide". A personal token will be generated as your access credential. You can manage your personal token in **Personal Account Settings** > **Access Token**.
![](https://qcloudimg.tencent-cloud.cn/raw/0328f4ffe65f64c73ddbf56115a076db.png)
After entering your login password, copy the configuration generated to the local `/etc/yum.repos.d/rpm-go.repo` file. If this file does not exist, create one.
![](https://qcloudimg.tencent-cloud.cn/raw/5c0bf0f57f4d342f05a1c4e8a270e20a.png)

## Push an Artifact[](#push)

Run the rpm publish command to push an RPM package.
<dx-codeblock>
:::  bash
curl -u [Username/Email] -X POST [Repository URL in the Push Guide] -T [Artifact Name].rpm
:::
</dx-codeblock>
After the artifact is pushed successfully, refresh the page to view the latest artifacts.

![](https://qcloudimg.tencent-cloud.cn/raw/7818e6318659e0b74d400acb55c5b064.png)

## Pull an Artifact[](#pull)

Run the command in the guide to pull an artifact.
![](https://qcloudimg.tencent-cloud.cn/raw/ae731ce6e7018de15824b89ab63d69ee.png)

## Configure a Proxy[](#proxy)

RPM repositories have a default proxy address. You can configure other addresses.
![](https://qcloudimg.tencent-cloud.cn/raw/f9ac309d688b85415d9f3c7bbe58c64a.png)

Configure the remote proxy repository URL, pull artifacts in the repository to the local machine, and the artifacts will be automatically backed up to CODING-AR.

<dx-alert infotype="explain" title="">
If CODING-AR does not automatically store RPM artifacts pulled from the proxy, check:
<ul style = "margin-bottom: 0px;"><li> Whether you have the permission to push artifacts to this repository.</li>
<li> Whether the artifacts already exist in your local cache.</li></ul>
</dx-alert>

