该文档介绍如何将 conan 类型制品存储在 CODING 制品库中，方便团队在项目进行统一的制品管理与版本控制。下文包含如何进行制品制作、认证配置与制品推拉。

## 进入制品仓库功能页

1. 登录 CODING 控制台，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击左侧菜单栏的**制品管理**，进入制品仓库功能页面。

## 准备工作

>! 阅读该篇文档需要准备好以下内容：
> -   安装 Python3。
> -   参见 [基础操作](https://intl.cloud.tencent.com/document/product/1136/44804) 创建制品仓库。
> -   制品仓库选择 conan 类型。

## 安装 Conan
使用 pip 安装，需要 python3.5 及以上的版本。
<dx-codeblock>
:::  bash
pip install
:::
</dx-codeblock>
使用 brew 安装。
<dx-codeblock>
:::  bash
brew install conan
:::
</dx-codeblock>

## 新建 conan 包[](id:init)
在本地新建 Demo 目录。
<dx-codeblock>
:::  bash
mkdir mypkg && cd mypkg
:::
</dx-codeblock>
创建 Demo 项目。
<dx-codeblock>
:::  bash
conan new hello/0.1 -t
:::
</dx-codeblock>
将项目打包成二进制包。
<dx-codeblock>
:::  bash
conan create . demo/testing
:::
</dx-codeblock>
如果执行报错 `/bin/sh: cmake: command not found`，需要执行命令安装 `cmake`。
<dx-codeblock>
:::  bash
$ pip3 install cmake
# 或
$ brew install cmake
:::
</dx-codeblock>


## 配置仓库认证信息[](id:config)
您可以选择自动生成配置或手动配置，下文以自动生成配置为例。

单击**页面指引**上的**使用访问令牌生成配置**，系统会帮您自动生成个人令牌作为访问凭证。您可以到**个人账户设置** > **访问令牌**进行管理。
![](https://qcloudimg.tencent-cloud.cn/raw/e7ba92bf2f106819553eb3fc40db64e2.png)
按照提示执行命令。
![](https://qcloudimg.tencent-cloud.cn/raw/ed5f7119beec7d16585d74b5c928b1d6.png)

## 推送制品
运行页面指引上的命令行，将变量替换为拟推送的制品名称与版本号。
<dx-codeblock>
:::  bash
conan upload [包名称]/[自定义版本号] --all -r=conan-go
:::
</dx-codeblock>


## 拉取制品
执行页面指引中的拉取命令，从当前仓库拉取制品。
<dx-codeblock>
:::  bash
conan install [包名称]/[自定义版本号]@ -r conan-go
:::
</dx-codeblock>

