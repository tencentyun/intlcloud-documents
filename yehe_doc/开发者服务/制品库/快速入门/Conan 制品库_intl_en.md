This document describes how to store Conan artifacts in CODING-AR for centralized artifact management and version control. The following sections introduce how to create an artifact, configure authentication, and pull and push artifacts.

## Open CODING-AR

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Artifact Management**.

## Preparations

>! Before you begin:
> -   Install Python3.
> -   Create an artifact repository (see [Basic Operations](https://intl.cloud.tencent.com/document/product/1136/44804)).
> -   Select Conan as the repository type.

## Install Conan
Python 3.5 or later is required to install Conan using pip.
<dx-codeblock>
:::  bash
pip install
:::
</dx-codeblock>
Install Conan with brew.
<dx-codeblock>
:::  bash
brew install conan
:::
</dx-codeblock>

## Create a Conan Package[](id:init)
Create a local demo directory.
<dx-codeblock>
:::  bash
mkdir mypkg && cd mypkg
:::
</dx-codeblock>
Create a demo project.
<dx-codeblock>
:::  bash
conan new hello/0.1 -t
:::
</dx-codeblock>
Build a binary package for the project.
<dx-codeblock>
:::  bash
conan create . demo/testing
:::
</dx-codeblock>
If an error message `/bin/sh: cmake: command not found` is displayed, run the following command to install `cmake`:
<dx-codeblock>
:::  bash
$ pip3 install cmake
# or
$ brew install cmake
:::
</dx-codeblock>


## Configure Authentication Information[](id:config)
You can select manual or automatic configuration. Automatic configuration is used in the following example.

Click **Generate configuration from access token** in "Guide". A personal token will be generated as your access credential. You can manage your personal token in **Personal Account Settings** > **Access Token**.
![](https://qcloudimg.tencent-cloud.cn/raw/e7ba92bf2f106819553eb3fc40db64e2.png)
Run the commands as prompted.
![](https://qcloudimg.tencent-cloud.cn/raw/ed5f7119beec7d16585d74b5c928b1d6.png)

## Push an Artifact
Run the command in the guide. Replace the variables with the name and version of the artifact to be pushed.
<dx-codeblock>
:::  bash
conan upload [package name]/[custom version number] --all -r=conan-go
:::
</dx-codeblock>


## Pull an Artifact
Run the pull command in the guide.
<dx-codeblock>
:::  bash
conan install [package name]/[custom vesion number]@ -r conan-go
:::
</dx-codeblock>

