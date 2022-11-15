>!本文档主要介绍 渠道合作伙伴 访问管理功能的相关内容，其他产品访问管理相关内容请参见 [支持 CAM 的产品](https://intl.cloud.tencent.com/document/product/598/10588)。

渠道合作伙伴访问管理实质上是将子帐号与策略进行绑定，或者说将策略授予子帐号。开发者可以在控制台上直接使用预设策略来实现一些简单的授权操作。

渠道合作伙伴目前提供了以下预设策略：

|策略名称|	策略描述|
| -------------- | ------------------------------------------------------------ |
|QcloudIntlpartnersmgtFullAccess|	渠道合作伙伴全读写访问权限|
|QcloudIntlpartnersmgtReadOnlyaccess|	渠道合作伙伴只读访问权限|

### 预设策略使用示例

#### 新建拥有渠道合作伙伴权限的子帐号

1、以腾讯云 [主帐号](https://www.tencentcloud.com/document/product/598/32633) 的身份访问 CAM 控制台的 [用户列表](https://console.cloud.tencent.com/cam)，单击**新建用户**。

2、在**新建用户**页面选择**自定义创建**，进入**新建子用户**页面。

>?请根据 [CAM 自定义创建子用户](https://intl.cloud.tencent.com/document/product/598/13674) 的操作指引完成**设置用户权限**之前的步骤。

#### 将渠道合作伙伴权限授予已存在的子帐号

1、以腾讯云 [主帐号](https://www.tencentcloud.com/document/product/598/32633) 的身份访问 CAM 控制台的 [用户列表](https://console.cloud.tencent.com/cam)，单击想要进行授权的子帐号。

2、单击**用户详情**页面权限栏的**添加策略**，如果子帐号的权限**非空**，则单击**关联策略**。

3、选择**从策略列表中选取策略关联**，搜索并勾选预设策略 "Intlpartnersmgt" 。后续按页面提示完成授权流程即可。

#### 解除子帐号的渠道合作伙伴权限

1、以腾讯云[主帐号](https://www.tencentcloud.com/document/product/598/32633)的身份访问 CAM 控制台的[用户列表](https://console.cloud.tencent.com/cam)，单击想要解除授权的子帐号。

2、在**用户详情**页面权限栏找到预设策略 "Intlpartnersmgt"，单击右侧的**解除**。按页面提示完成解除授权流程即可。

