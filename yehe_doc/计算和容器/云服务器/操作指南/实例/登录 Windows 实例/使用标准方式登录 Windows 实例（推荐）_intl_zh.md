## 操作场景
本文介绍如何使用标准登录方式（WebRDP）登录 Windows 实例。 

<dx-alert infotype="explain" title="">
该方式不区分本地机器操作系统，支持通过控制台直接登录 Windows 实例。
</dx-alert>



## 前提条件[](id:Prerequisites)
- 已获取远程登录 Windows 实例需要使用实例的管理员帐号和对应的密码。
 - 如已设置登录密码，则请使用该密码登录。如忘记密码，则请 [重置实例密码](https://intl.cloud.tencent.com/document/product/213/16566)。
 - 如在创建实例时选择系统随机生成密码，则请往 [站内信](https://console.cloud.tencent.com/message) 获取初始密码。
- 您的云服务器实例已购买公网 IP，且已在实例关联的安全组中放通来源为 WebRDP 代理 IP 的远程登录端口（默认为3389）。
 - 如通过快速配置购买云服务器，则默认已开通。
 - 如通过自定义配置购买云服务器，则可参考 [允许 RDP 远程连接 Windows 云服务器](https://intl.cloud.tencent.com/document/product/213/32369) 手动放通。
- 请确保您实例的公网带宽 ≥ 5Mbit/s，否则会引起远程桌面卡顿。如需调整网络带宽，请参见 [调整网络配置](https://intl.cloud.tencent.com/document/product/213/15517)。


## 操作步骤

1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/index)。
2. 在实例的管理页面，根据实际使用的视图模式进行操作：
<dx-tabs>
::: 列表视图
找到需要登录的 Windows 云服务器，单击右侧的**登录**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)

:::
::: 页签视图
选择需要登录的 Windows 云服务器页签，单击**登录**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)

:::
</dx-tabs>
3. 在打开的“标准登录 | Windows 实例”窗口中，根据实际情况填写登录信息。
 - **端口**：默认为3389，请按需填写。
 - **用户名**：Windows 实例用户名默认为 `Administrator`，请按需填写。
 - **密码**：填写已从 [前提条件](#Prerequisites) 步骤中获取的登录密码。
5. 单击**登录**，即可登录 Windows 实例。
本文以登录操作系统为 Windows Server 2016 数据中心版64位英文版的云服务器为例，登录成功则出现类似如下图所示界面：
![](https://main.qcloudimg.com/raw/60abc6a9f51ae33ea95aa11edc53e009.jpg)


## 相关文档
- [重置实例密码](https://intl.cloud.tencent.com/document/product/213/16566)
- [调整网络配置](https://intl.cloud.tencent.com/document/product/213/15517)
