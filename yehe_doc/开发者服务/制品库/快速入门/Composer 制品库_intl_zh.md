本文档介绍如何快速使用 Composer 制品仓库，方便团队在项目进行统一的制品管理与版本控制。内容包含如何进行制品包制作、认证配置与制品推拉。

## 进入制品仓库功能页

1. 登录 [CODING 控制台](https://console.cloud.tencent.com/coding)，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击左侧菜单栏的**制品管理**，进入制品仓库功能页面。

## 准备工作

>! 阅读该篇文档需要准备好以下内容：
> -   安装 Composer。
> -  参见 [基础操作](https://intl.cloud.tencent.com/document/product/1136/44804) 创建制品仓库。
> -   制品仓库选择 Composer 类型。

## 制作 Composer 包（可选阅读）[](id:composer)

### 安装 Composer
在终端中执行下载 Copmoser 命令。
<dx-codeblock>
:::  bash
curl -sS https://getcomposer.org/installer | php
:::
</dx-codeblock>
添加至环境变量，方便全局运行命令。
<dx-codeblock>
:::  bash
mv composer.phar /usr/local/bin/composer
:::
</dx-codeblock>


### 初始化[](id:init)
新建 Demo 目录。
<dx-codeblock>
:::  bash
mkdir composer-demo && cd composer-demo
:::
</dx-codeblock>
初始化 Composer 包，按照提示输入初始化信息。
<dx-codeblock>
:::  bash
composer inits
:::
</dx-codeblock>
初始化完成后会在同一目录下新增 `composer.json` 文件作为该 Composer 包的配置文件。

## 配置认证文件
前往 Composer 包的文件目录，新建 `auth.json` 文件。您可以使用自动生成配置或手动配置两种方式进行配置。

### 自动生成配置
单击网页上的**使用访问令牌生成配置**按钮，复制内容后粘贴至 `auth.json` 文件内。
![](https://qcloudimg.tencent-cloud.cn/raw/de3c2d8f5e423d7ed9120c8e63920b2a.png)

### 手动配置
复制网页上的命令，并将其中的 `[PASSWORD]` 替换为您的服务密码。

## 推送
根据 CODING 制品库页面给出的推送命令，将 Composer 包文件打包成 `zip` 并使用 `cURL` 等工具推送至仓库。
![](https://qcloudimg.tencent-cloud.cn/raw/2099fd7d7ae9093514680135a78c54a8.png)
推送时需按照提示输入您在 `auth.json` 文件中填写的密码，并将 `<version>` 替换为拟定的版本号。
![](https://qcloudimg.tencent-cloud.cn/raw/bbdee0cef010657e77dce17be10fb0e3.png)
推送完成后即可在 CODING  制品库看到已推送的包。
![](https://qcloudimg.tencent-cloud.cn/raw/995c325e351c4ad52eba95ef47817d5e.png)

## 拉取
进入 Composer 包的文件目录，设置仓库地址。相关命令已在 CODING 页面生成。
![](https://qcloudimg.tencent-cloud.cn/raw/e3920b43e9582a9edaec8d8ec5e13aba.png)

使用 CODING 制品库代替 Composer 官方的源（可选）。
<dx-codeblock>
:::  bash
composer config repo.packagist false
:::
</dx-codeblock>
执行拉取命令，将 `<package>` 包替换为拟拉取的包。
<dx-codeblock>
:::  bash
composer require < PACKAGE >:< VERSION >
:::
</dx-codeblock>
输入服务邮箱与密码后成功拉取。
<img src = "https://qcloudimg.tencent-cloud.cn/raw/1a0558b99d6698d8a763d16191f3481c.png" style="width: 100%">

## 设置代理
当 CODING 私有制品仓库不存在想要拉取的制品时，将尝试从配置的代理地址拉取。您可以添加第三方制品源，用以获取特定仓库中的制品。无需额外设置，CODING 将会按照顺序从上到下依次检索相应的制品包。
![](https://qcloudimg.tencent-cloud.cn/raw/9d9df265987bbbedd471f71a46dbb009.png)

