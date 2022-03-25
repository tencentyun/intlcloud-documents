## 操作场景
WebShell 为腾讯云推荐的登录方式。无论您的本地系统为 Windows，Linux 或者 Mac OS，只要实例购买了公网 IP，都可以通过 WebShell 登录。本文介绍如何使用标准登录方式（WebShell）登录 Linux 实例。
WebShell 优点如下：
- 支持快捷键复制粘贴。
- 支持鼠标滚屏。
- 支持中文输入法。
- 安全性高，每次登录需要输入密码或密钥。

## 鉴权方式

**密码**或**密钥**

## 前提条件[](id:Prerequisites)

- 已获取登录 Linux 实例的管理员帐号及密码（或密钥）。
 - 如在创建实例时选择系统随机生成密码，则请前往 [站内信](https://console.cloud.tencent.com/message) 获取。
 - 如已设置登录密码，则请使用该密码登录。如忘记密码，则请 [重置实例密码](https://intl.cloud.tencent.com/document/product/213/16566)。
 - 如已给实例绑定密钥，则可使用密钥登录。如需进一步了解密钥，请参考 [SSH 密钥](https://intl.cloud.tencent.com/document/product/213/6092)。
- 您的云服务器实例已购买公网 IP，且已在实例关联的安全组中放通来源为 WebShell 代理 IP 的远程登录端口（默认为22）。
 - 如通过快速配置购买云服务器，则默认已开通。
 -  如通过自定义配置购买云服务器，则可参考 [允许 SSH 远程连接 Linux 云服务器](https://intl.cloud.tencent.com/document/product/213/32369) 手动放通。

## 操作步骤

1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/index)。
2. 在实例的管理页面，根据实际使用的视图模式进行操作：
<dx-tabs>
::: 列表视图
找到需要登录的 Linux 云服务器，单击右侧的**登录**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)

:::
::: 页签视图
选择需要登录的 Linux 云服务器页签，单击**登录**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)

:::
</dx-tabs>

3. 在打开的“标准登录 | Linux 实例”窗口，根据实际需求选择**密码登录**或者**密钥登录**方式进行登录。如下图所示：
![](https://main.qcloudimg.com/raw/9c321ad519c8f993c1f768e56fca0ab1.png)
请参考以下说明填写登录所需信息：
 -  **端口**：默认为22，请按需填写。
 -  **用户名**：Linux 实例用户名默认为 root（Ubuntu 系统实例用户名默认为 ubuntu），请按需填写。
 -  **密码**：填写已从 [前提条件](#Prerequisites) 步骤中获取的登录密码。
 - **密钥**：选择已绑定实例的密钥。
4. 单击**登录**，即可登录 Linux 实例。
如果登录成功，WebShell 界面会出现如下提示。如下图所示：
![](https://main.qcloudimg.com/raw/6bcd152ff947909f52da67430aa7eda6.png)

## 后续操作

当您成功登录云服务器后，您可以在腾讯云服务器上搭建个人站点，论坛或者使用其他操作。相关操作可参考：
- [搭建 WordPress 个人站点](https://intl.cloud.tencent.com/document/product/213/8044)
- [搭建 Discuz! 论坛](https://intl.cloud.tencent.com/document/product/213/8043)


## 相关文档
- [重置实例密码](https://intl.cloud.tencent.com/document/product/213/16566)
- [管理 SSH 密钥](https://intl.cloud.tencent.com/document/product/213/16691)
