This document describes how to store CocoaPods artifacts in CODING-AR for centralized artifact management and version control. The following sections introduce how to create an artifact, configure authentication, and pull and push artifacts.

## Open CODING-AR

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Artifact Management**.

## Preparations

>! Before you begin:
> -   Install CocoaPods.
> -   Create an artifact repository (see [Basic Operations](https://intl.cloud.tencent.com/document/product/1136/44804)).
> -   Select CocoaPods as the repository type.

## Install CocoaPods[](id:install)
Run either of the following commands to install CocoaPods.
<dx-codeblock>
:::  bash
$ sudo gem install cocoapods
-- or
$ brew install cocoapods
:::
</dx-codeblock>


## Create a Demo Project[](id:init)
This section describes how to quickly create a demo CocoaPods artifact. You can skip this section if you are familiar with CocoaPods artifacts.

Run the following command in a directory and select a template as needed when asked.
<dx-codeblock>
:::  bash
pod lib create <custom pod name>
:::
</dx-codeblock>
The sample CocoaPods code will be cloned from GitHub to your local machine.

## Configure Authentication Information
Install the CODING CocoaPods plugin.
<dx-codeblock>
:::  bash
sudo gem install cocoapods-coding-ar
:::
</dx-codeblock>
You can select manual or automatic configuration. Automatic configuration is used in the following example. Click **Generate configuration from access token** in "Guide". A personal token will be generated as your access credential. You can manage your personal token in **Personal Account Settings** > **Access Token**.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/3311ec6ba788b4cedc51e0bf533b69fe.png" style="width: 100%">
Copy the commands to your `~/.netrc` file. If this file does not exist, run `vim ~/.netrc` to create it and then copy the commands.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/006cb67a528bb10591b7455f0d90166f.png" style="width: 100%">


## Push an Artifact
Run the commands in the guide.
![](https://qcloudimg.tencent-cloud.cn/raw/c00938a8836e970a7a15226633feac78.png)

## Pull an Artifact
Pull a specific CocoaPods artifact by referring to the specific guide.

1.  Modify the Podfile.
<dx-codeblock>
:::  bash
source '<repository URL in the guide>'
target 'MyApp' do
    pod '<Artifact Name>', '~> <Version>'
end
:::
</dx-codeblock>
2.  Run the pull command.
<dx-codeblock>
:::  bash
pod install
:::
</dx-codeblock>
