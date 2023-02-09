为方便您快速接入腾讯云游戏多媒体引擎，本文主要为您介绍如何进行应用创建与服务开通。

## 新建应用

[](id:test1)

1. 登录 [游戏多媒体引擎控制台](https://console.intl.cloud.tencent.com/gamegme)，单击左侧菜单**服务管理**，进入服务管理页面。
2. 在服务管理页面，单击**新建应用**。
![](https://qcloudimg.tencent-cloud.cn/raw/f687244df3c633d9a873c58aec4bf864.png)
3. 填写应用的相关信息。
  ![](https://qcloudimg.tencent-cloud.cn/raw/7fac1c705952f11b994e4769b964d803.png)
   - 应用名称：创建应用名称，建议创建有意义的应用名称以便在列表中被轻松识别。
   - 所属项目：默认为腾讯云的“默认项目”，同时您也可以创建项目进行选择，详情可参见 [项目管理 - 新建项目](https://www.tencentcloud.com/zh/document/product/378/34726#.E6.96.B0.E5.BB.BA.E9.A1.B9.E7.9B.AE)。
   - 标签：单击“+添加”可进行添加标签，标签新增详情可参见 [标签管理](#test)。
4. 按照需要选择所需的服务。
   - 开启或关闭**实时语音服务**
    实时语音服务按语音时长计费，您可根据需求进行开启。
   ![](https://qcloudimg.tencent-cloud.cn/raw/d8986ba5724ee54e2824d917e74a64d6.png)
   - 开启或关闭**语音消息服务**
   语音消息服务按 DAU 计费，您可根据需求进行开启。
   ![](https://qcloudimg.tencent-cloud.cn/raw/54770276d70bdffaee0c5d9f19d5df83.png)
   - 开启或关闭**语音转文本服务**
   语音转文本服务按时长计费，您可根据需求进行开启。
	![](https://qcloudimg.tencent-cloud.cn/raw/851315bafd172e1c830ead5fbe78a8a7.png)
5. 勾选“我已阅读并同意游戏多媒体引擎 [服务等级协议](https://www.tencentcloud.com/zh/document/product/607/30455) 和 [SDK隐私协议](https://www.tencentcloud.com/zh/document/product/607/37524)”。
6. 单击**确定**即可成功创建应用。



## 设置应用

新建应用后，应用将在服务管理页面的“应用列表”中展示，单击**设置**进入应用详情页。
![](https://qcloudimg.tencent-cloud.cn/raw/5030bd1d74a6ee68fb414ca1644037fd.png)

### 修改应用信息

1. 单击“应用信息”中的**修改**后，可对相应信息进行修改。
2. 修改完成后，单击**保存**。
![](https://qcloudimg.tencent-cloud.cn/raw/4027bcb5db4cdf5c17b07bf305832e69.png)

### 修改服务状态

1. 单击对应服务中的**修改**后，可对服务的开启或关闭状态进行修改。
2. 修改完成后，点击**保存**。
![](https://qcloudimg.tencent-cloud.cn/raw/e28d05b92ccda7aa011764800a5f3a50.png)

## 重点参数

在“鉴权信息”中可获取到使用 SDK 语音服务时所需要的参数 AppID 以及权限密钥。
![](https://qcloudimg.tencent-cloud.cn/raw/667413c114bec5fc5f73cb0f08c3d472.png)

> ?
- 此模块中的权限密钥将会作为参数使用到 SDK 接入过程中。 
- 重置密钥后，15分钟 - 1小时内生效，不建议频繁更换。
- 只有创建游戏的账号、主账号、全局协作者可以操作**重置密钥**。
- 鉴权详细使用请参考[鉴权密钥](https://www.tencentcloud.com/zh/document/product/607/12218)。



[](id:test)

## 标签管理

在 [新建应用](#test1) 时如需进行标签添加，单击“+添加”即可为应用设置已有的标签。如果未创建标签，可按如下步骤先完成标签创建：

1. 在新建应用的应用信息页面，单击 **[标签管理](https://console.intl.cloud.tencent.com/tag/taglist)** 进入标签列表页。
![](https://qcloudimg.tencent-cloud.cn/raw/2675330a883aefeeaa2c0ad6f374afb7.png)
2. 单击**新建标签**进入“新建标签”页面，填写相关信息。
![](https://qcloudimg.tencent-cloud.cn/raw/81a09412f346f0df5f3e5c94dd03f5b0.png)
3. 单击**确定**即可成功创建标签。

## 停用服务

目前已经创建的应用无法删除，如后续不使用该应用，则关闭当前应用下的所有服务即可。关闭服务后，该应用的所有请求将立即失败，请谨慎停用，避免对线上业务造成影响。关闭服务需手动进入 [游戏多媒体引擎控制台](https://console.intl.cloud.tencent.com/gamegme)，在对应 AppID 的应用中单击**设置**进入应用详情页面。
![](https://qcloudimg.tencent-cloud.cn/raw/5030bd1d74a6ee68fb414ca1644037fd.png)
选择对应的服务单击**修改** > **关闭** > **保存**，即可停止服务。
![](https://qcloudimg.tencent-cloud.cn/raw/887c4e50e5f22b32bc08f9f4d712f80c.png)