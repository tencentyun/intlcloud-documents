This document describes how to store NuGet artifacts in CODING-AR for centralized artifact management and version control. The following sections introduce how to create an artifact repository and NuGet package, pull and push artifacts, and configure proxies.

## Open CODING-AR

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Artifact Management**.

## Preparations

>! Before you begin:
> -   Install NuGet.
> -   Create an artifact repository (see [Basic Operations](https://intl.cloud.tencent.com/document/product/1136/44804)).
> -   Select NuGet as the repository type.

## Initialize a NuGet Artifact (Optional) [](#init)

Visit the [NuGet website](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools#macoslinux) to and download and install NuGet.

### Generate a NuGet artifact locally[](#local)

You can skip this section if you are familiar with NuGet artifacts.

1.  Create a demo directory.
<dx-codeblock>
:::  bash
mkdir nuget-demo && cd nuget-demo
:::
</dx-codeblock>
2.  Create a `.nuspec` package.
<dx-codeblock>
:::  nuget
nuget spec [Artifact Name]
:::
</dx-codeblock>
3.  Package the artifact.
<dx-codeblock>
:::  nuget
nuget pack <Artifact Name>.nuspec
:::
</dx-codeblock>
4.  After the artifact is packaged, you can view the package file generated in the local directory.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/ec7b5108396ce4546b58ac767800edfb.png" style="width: 100%">


### Pull an artifact from an online source[](#online)

Visit the [NuGet website](https://www.nuget.org/packages), search for a NuGet artifact, and download it or pull it via the command line.
![](https://main.qcloudimg.com/raw/348052025659e19d2527aa293170d31e.png)

Pull an artifact via the command line:
<dx-codeblock>
:::  nuget
nuget install [Artifact Name] -OutputDirectory packages
:::
</dx-codeblock>

## Configure Authentication Information[](#auth)

Authentication information must be configured before you can pull artifacts from or push artifacts to CODING-AR. The following example uses **automatic configuration**.

Click **Generate configuration from access token** and enter your password to obtain the configuration command. Then, copy and run the command in the directory where the NuGet artifact is stored. During this process, **permission control** is implemented with the **personal access token**.
![](https://qcloudimg.tencent-cloud.cn/raw/5a0467096aac7a820f5cd307233d30a0.png)


## Push an Artifact[](#push)

Replace the variables and run the command push an artifact.
<dx-codeblock>
:::  bash
nuget push -ApiKey api -Source [Repository name in the push guide] [Local artifact name].nupkg
:::
</dx-codeblock>

## Pull an Artifact[](#pull)

Replace the variables and run the command pull an artifact.
<dx-codeblock>
:::  bash
nuget install -Source [Repository name in the pull guide] -Version [Artifact Version] [Artifact Name]
:::
</dx-codeblock>


## Configure a Proxy[](#proxy)

If you try to pull an artifact that does not exist in the CODING private repository, the system will try to pull from the configured proxy. You can add a third-party artifact source to obtain artifacts from the specific repository. Without the need for configuration, CODING will retrieve artifacts in sequence from top to bottom.
![](https://qcloudimg.tencent-cloud.cn/raw/fb57fe7d421c38bcfd2ca099304914b5.png)

Run the following command to pull an artifact:
<dx-codeblock>
:::  bash
nuget install -Source [Repository Name] -Version [Artifact Version] [Artifact Name]
:::
</dx-codeblock>
<img src = "https://qcloudimg.tencent-cloud.cn/raw/7f507386eea62b36ba2a4c92d2610d8b.png" style="width: 100%">
The artifact and its dependencies will be pulled to the local machine and synchronized to CODING-AR. The package source will be shown on the details page.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/3c9af80f439c4fee109fc7800e295a62.png" style="width: 100%">
<dx-alert infotype="explain" title="">
If CODING-AR does not automatically store NuGet artifacts pulled from the proxy, check:
<ol style = "margin-bottom: 0px;"><li>Whether you have the permission to push artifacts to this repository.</li>
<li>Whether the artifacts already exist in your local cache.</li></ol>
</dx-alert>



