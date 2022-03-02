该文档介绍如何将 Helm 类型的制品存储在 CODING 制品库中。其内容包括创建制品库、推送、拉取和删除制品。

## 进入制品仓库功能页

1. 登录 [CODING 控制台](https://console.cloud.tencent.com/coding)，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击左侧菜单栏的**制品管理**，进入制品仓库功能页面。

## 准备工作

>! 阅读该篇文档需要准备好以下内容：
> -   [安装 Helm](https://helm.sh/docs/intro/install/)。
> -   参见 [基础操作](https://intl.cloud.tencent.com/document/product/1136/44804) 创建制品仓库。
> -   制品仓库选择 Helm 类型。

## 制作包（可选阅读）[](id:helm-chart)

本章节提供两种方法快速创建一个 Helm Chart，若您已熟悉制作方法可跳过本节。


### 方法一：本地制作镜像

1.  在本地任意目录创建 Helm Chart 并自定义包名。
<dx-codeblock>
:::  bash
helm create [name]
:::
</dx-codeblock>
2.  打包。
<dx-codeblock>
:::  bash
helm package [name]
:::
</dx-codeblock>


### 方法二：直接拉取 artifacthub 中的制品

搜索任意 Helm Chart 并在本地自定义目录下运行下载命令。
<dx-codeblock>
:::  bash
$ helm repo add [远程仓库名] [远程仓库地址]
$ helm fetch [helm chart 在远程仓库的地址>]--version [版本]
:::
</dx-codeblock>
<img src = "https://qcloudimg.tencent-cloud.cn/raw/518e2fd7cb306339c65cbeee968b30ef.png" style="width: 100%">
运行成功后本地会出现相关制品。
<img src = "https://qcloudimg.tencent-cloud.cn/raw/53bddcf86307385da0c171be24188ec1.png" style="width: 100%">

## 配置认证信息

在本地完成制品编译后，就可以将制品推送至远端制品仓库。推送之前需在本地配置远端仓库的认证信息。您可以按照**页面指引**，选择 Helm+ cURL 或 Helm + CODING Helm 插件两种方法进行制品推拉。
![](https://qcloudimg.tencent-cloud.cn/raw/83ebfcefe7e1d723cc4650db4a9d6198.png)

**下文以 CODING 插件为例：**
![](https://qcloudimg.tencent-cloud.cn/raw/799fc2f4f7767eedfde59bf39013033b.png)

复制页面指引上的命令在本地安装插件后，单击**使用访问令牌生成配置**按钮并复制命令，使用终端在相应的包目录执行配置命令。
![](https://qcloudimg.tencent-cloud.cn/raw/bb00440085580baecfd9f20f8fc3d110.png)

## 推送制品

进入 Helm Chart 所在目录，并执行**页面指引**中的命令，即可把指定的 Helm Chart 推送至制品库：
<dx-codeblock>
:::  bash
helm push [制品包名.tgz] [推送指引中的仓库信息]
:::
</dx-codeblock>
推送成功后，刷新仓库页面即可看到最新推送的制品。
<img src = "https://qcloudimg.tencent-cloud.cn/raw/7367093d697f41a8eb4cab8359d01f57.png" style="width: 100%">


## 拉取制品

如果您的制品仓库有更新，拉取前可以执行命令更新。
<dx-codeblock>
:::  bash
helm repo update
:::
</dx-codeblock>
更新后执行拉取命令。
<dx-codeblock>
:::  bash
helm fetch [拉取指引中的制品信息] --version [版本]
:::
</dx-codeblock>
