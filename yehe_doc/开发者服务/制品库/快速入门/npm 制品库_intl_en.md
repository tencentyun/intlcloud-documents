This document describes how to store npm artifacts in CODING-AR for centralized artifact management and version control. The following sections introduce how to create an artifact, configure authentication, and pull and push artifacts.

## Open CODING-AR

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Artifact Management**.

## Preparations

>! Before you begin:
> -   Install Node.js.
> -   Create an artifact repository (see [Basic Operations](https://intl.cloud.tencent.com/document/product/1136/44804)).
> -   Select npm as the repository type.

## Initialize a Local npm Project (Optional)

You can skip this section if you are familiar with npm artifacts.

1.  Create a demo directory for the npm project.
<dx-codeblock>
:::  bash
mkdir npm-demo
:::
</dx-codeblock>
2.  Initialize the npm project.
<dx-codeblock>
:::  bash
cd npm-demo && npm init
:::
</dx-codeblock>
Enter the npm configuration in the new `package.json` when asked. For example:
<dx-codeblock>
:::  json
{
    "name": "example",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "author": "",
    "license": "MIT"
}
:::
</dx-codeblock>
3.  Create a `.npmrc` file.
<dx-codeblock>
:::  bash
touch .npmrc
:::
</dx-codeblock>


## Configure Authentication Information

Authentication information must be configured before you can pull artifacts from or push artifacts to CODING-AR.

Configure authentication information in either of the following ways:
-   Set credentials with the configuration file
-   Set credentials with the interactive command line

### Method 1: setting credentials with configuration file

1.  On the guide page, click **Generate configuration from access token** and enter the account login password in the pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/ba2cc20f43738f5d3b1108ffa114d14c.png)
2.  Copy the configuration to the `.npmrc` file in the same directory as your project's `package.json`.
![](https://qcloudimg.tencent-cloud.cn/raw/9b658b97e88c19cc44dbb0323b86e3ab.png)

### Method 2: set credentials with interactive command line

1.  Copy and run the `npm config` to set the `npm registry` to the current artifact repository.
![](https://qcloudimg.tencent-cloud.cn/raw/a99222527a31017b414a758ebd584bbd.png)
2.  Run `npm login` and enter the account, password, and email address when asked.
<dx-codeblock>
:::  bash
npm login
:::
</dx-codeblock>


## Push an npm Artifact

Copy and run the **push** command on the page to push a local artifact to the remote repository.
<dx-codeblock>
:::  bash
npm publish --registry=<Repository URL in the Push Guide>
:::
</dx-codeblock>
<img src = "https://main.qcloudimg.com/raw/0b890f246781554db6e7e7f020ad9314.png" style="width: 100%">
After the artifact is pushed successfully, refresh the page to view the latest artifacts.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/e52a684d0c89d1d4a8e3f5f3c6da637e.png" style="width: 100%">


## Pull an npm Artifact

Copy and run the `npm install` command to pull an artifact:
![](https://qcloudimg.tencent-cloud.cn/raw/cd88f16bd0fd9c3dcedf5ae969690278.png)
<dx-codeblock>
:::  bash
npm install <Package Name> --registry=<Repository URL in the Pull Guide>
:::
</dx-codeblock>
After the artifact is pulled, you can see a success message.
<img src = "https://main.qcloudimg.com/raw/072e89fdcb9f0ff83dbb08a7473191d3.png" style="width: 100%">


## Configure a Proxy

If you try to pull an artifact that does not exist in the CODING private repository, the system will try to pull from the configured proxy. You can add a third-party artifact source to obtain artifacts from the specific repository. Without the need for configuration, CODING will retrieve artifacts in sequence from top to bottom.
![](https://qcloudimg.tencent-cloud.cn/raw/71da9c4d5139a9a0229af58e855f2a70.png)
Replace `<package>` with the package name and run the command generated on the page to pull the package.
![](https://qcloudimg.tencent-cloud.cn/raw/cd88f16bd0fd9c3dcedf5ae969690278.png)
The artifact and its dependencies will be pulled to the local machine and synchronized to CODING-AR. The package source will be shown on the details page.
![](https://qcloudimg.tencent-cloud.cn/raw/163e3af5ee49a78e78a20778b0e01be9.png)

