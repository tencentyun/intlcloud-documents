This document describes how to store Helm artifacts in CODING-AR, including how to create a repository and push, pull, and delete artifacts.

## Open CODING-AR

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Artifact Management**.

## Preparations

>! Before you begin:
> -   [Install Helm](https://helm.sh/docs/intro/install/).
> -   Create an artifact repository (see [Basic Operations](https://intl.cloud.tencent.com/document/product/1136/44804)).
> -   Select Helm as the repository type.

## Create a Package (Optional) [](id:helm-chart)

This section describes how to quickly create a Helm chart. You can skip this section if you are familiar with Helm charts.


### Method 1: create an image locally

1.  In a local directory, create a Helm chart.
<dx-codeblock>
:::  bash
helm create [name]
:::
</dx-codeblock>
2.  Package the chart.
<dx-codeblock>
:::  bash
helm package [name]
:::
</dx-codeblock>


### Method 2: pull an artifact from Artifact Hub

Search for a Helm chart and run the download command in a local directory.
<dx-codeblock>
:::  bash
$ helm repo add [Remote Repository Name] [Remote Repository URL]
$ helm fetch [Helm Chart URL in the Remote Repository>]--version [Version]
:::
</dx-codeblock>
<img src = "https://qcloudimg.tencent-cloud.cn/raw/518e2fd7cb306339c65cbeee968b30ef.png" style="width: 100%">
After the commands are successfully run, you can view the artifact locally.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/53bddcf86307385da0c171be24188ec1.png" style="width: 100%">

## Configure Authentication Information

After creating a local artifact, you can push it to the remote repository. Before the push, you need to locally configure the authentication information of the remote repository. You can pull or push an artifact by using Helm + cURL or Helm + CODING Helm plugin as instructed in the **Guide**.
![](https://qcloudimg.tencent-cloud.cn/raw/83ebfcefe7e1d723cc4650db4a9d6198.png)

**The following example uses the CODING Helm plugin:**
![](https://qcloudimg.tencent-cloud.cn/raw/799fc2f4f7767eedfde59bf39013033b.png)

Copy and run the command in the guide to install the plugin. Then click **Generate configuration from access token**, and copy and run the configuration command in the package directory.
![](https://qcloudimg.tencent-cloud.cn/raw/bb00440085580baecfd9f20f8fc3d110.png)

## Push an Artifact

Go to the directory where the Helm chart is stored and run the command in the **Guide** to push the specified Helm chart to the repository.
<dx-codeblock>
:::  bash
helm push [Package Name.tgz] [Repository Info in the Push Guide]
:::
</dx-codeblock>
After the artifact is pushed successfully, refresh the page to view the latest artifacts.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/7367093d697f41a8eb4cab8359d01f57.png" style="width: 100%">


## Pull an Artifact

If your artifact repository is updated, run the update command before pulling an artifact.
<dx-codeblock>
:::  bash
helm repo update
:::
</dx-codeblock>
After the update is successful, run the pull command.
<dx-codeblock>
:::  bash
helm fetch [Artifact Info in the pull guide] --version [Version]
:::
</dx-codeblock>
