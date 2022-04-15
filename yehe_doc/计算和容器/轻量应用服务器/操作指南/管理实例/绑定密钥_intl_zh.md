## 操作场景
本文介绍如何通过控制台在轻量应用服务器实例详情页面，将指定密钥绑定至实例。

## 前提条件
- 仅支持绑定密钥至 Linux 实例。
- 创建并保存密钥，详情请参见 [创建 SSH 密钥](https://intl.cloud.tencent.com/document/product/1103/41392#directions)。

## 操作步骤

1. 登录 [轻量应用服务器控制台](https://console.cloud.tencent.com/lighthouse/instance/index)，并单击需绑定密钥的实例卡片。
2. 在实例详情页中，选择**密钥对**页签，并单击**绑定密钥对**。
3. 在弹出的“绑定密钥”窗口中，根据实例状态进行操作：
<dx-tabs>
::: 实例“运行中”
1. 在“选择密钥”步骤中，勾选需绑定密钥，并单击**下一步**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/ee7c7af4b10044247662566d22b72839.png)
2. 在“关机提示”步骤中，勾选“同意强制关机”并单击**确定**即可。
<dx-alert infotype="explain" title="">
- 绑定过程中，实例将会先关机再开机。其期间将会短暂中断业务，建议您在业务低谷时操作。
- 如果正常关机失败，则会进行强制关机。强制关机可能会导致数据丢失或文件系统损坏，请谨慎操作！
- 强制关机可能需要您等待较长时间，请耐心等待。
</dx-alert>



:::
::: 实例“已关机”
1. 在“选择密钥”步骤中，勾选需绑定密钥，并单击**下一步**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/4dea54103d35df0af4d507f3f4b892de.png)
2. 在“关机提示”步骤中，单击**确定**即可。
:::
</dx-tabs>
<dx-alert infotype="notice" title="">
为提高轻量应用服务器实例的安全性，Linux 实例绑定密钥后，会默认禁止通过密码登录 root 用户。如您仍需保留密码登录方式，可参考 [修改 SSH](https://intl.cloud.tencent.com/document/product/1103/41392#.3Ca-id.3D.22changessh.22.3Emodifying-ssh-configuration.3C.2Fa.3E) 进行修改。
</dx-alert>

## 相关操作
### 解绑密钥
1. 登录 [轻量应用服务器控制台](https://console.cloud.tencent.com/lighthouse/instance/index)，并单击需绑定密钥的实例卡片。
2. 在实例详情页中，选择**密钥对**页签。
3. 勾选需解绑的密钥对，单击列表上方的**解绑**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/d7de6a4e40b97f0dfb825bf2b29e6df8.png)
4. 在弹出的“解绑密钥”窗口中，根据实例状态进行操作：
<dx-tabs>
::: 实例“运行中”
1. 在“选择密钥”步骤中，确认解绑密钥并单击**下一步**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/1747313d9fff9892263985870321e988.png)
2. 在“关机提示”步骤中，单击**确定**即可。
:::
::: 实例“已关机”
1. 在“选择密钥”步骤中，确认解绑密钥并单击**下一步**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/cf24adacd0a8f3a5be5648d70cb9e6c9.png)
2. 在“关机提示”步骤中，单击**确定**即可。
:::
</dx-tabs>


## 相关文档
- [管理密钥](https://intl.cloud.tencent.com/document/product/1103/41392)
- [使用远程登录软件登录 Linux 实例](https://intl.cloud.tencent.com/document/product/1103/41524)
- [使用 SSH 登录 Linux 实例](https://intl.cloud.tencent.com/document/product/1103/41525)
