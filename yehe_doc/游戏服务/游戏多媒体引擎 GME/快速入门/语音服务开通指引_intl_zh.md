为方便您快速接入腾讯云游戏多媒体引擎产品，本文为您介绍适用于游戏多媒体引擎 SDK 的语音服务申请指引。

## 新建服务

<span id="test1"></span>

### 新建应用

1. 登录 [游戏多媒体引擎控制台](https://console.cloud.tencent.com/gamegme)，单击左侧菜单【服务管理】，进入服务管理页面。
2. 单击【新建应用】，填写应用的相关信息，按照需要选择所需的服务。
![](https://main.qcloudimg.com/raw/fe3666053156cd53c29053b851ea5b6f.png)
3. 填写应用信息。
![](https://main.qcloudimg.com/raw/0d5da346fcbbad3b938fd86bd707087f.png)
   - 应用名称：创建应用名称，建议创建有意义的应用名称以便在列表中被轻松识别。
   - 所属项目：默认为腾讯云的“默认项目”，同时您也可以创建项目进行选择，详情可参见 [新建项目](https://intl.cloud.tencent.com/document/product/378/34726)。
   - 标签：单击“+添加”可进行添加标签，标签新增详情可参见 [标签管理](#test)。
4. 开启或关闭**实时语音服务**。
 **实时语音服务**按语音时长计费，您可根据需求进行开启，并到 [购买页](https://intl.cloud.tencent.com/zh/document/product/607/36276) 进行购买。
![](https://main.qcloudimg.com/raw/6360fc755f9b7f3893064b719a71da31.png)
5. 开启或关闭**语音消息及转文本服务**。
您可根据需求进行开启并选择对应转文本支持语言的模式，不同模式单价不同，详情可参见 [计费规则](https://intl.cloud.tencent.com/document/product/607/36276)。
![](https://main.qcloudimg.com/raw/09e232363c701db84059b887626aa5ed.png)
7. 单击【确定】 即可成功创建应用。



## 设置服务

新建应用后，应用将在“应用列表”中展示，单击【设置】进入应用详情页。
![](https://main.qcloudimg.com/raw/2b91bfdb40f81c3a3aed498ce8077961.png)

### 设置应用

单击“应用信息”中的【修改】后可对相应信息进行修改。
![](https://main.qcloudimg.com/raw/12391b6b0ca03f79348cd390d749f39e.png)

### 开启关闭业务

单击实时语言服务的【修改】后可对业务及服务进行开启或者关闭。
![](https://main.qcloudimg.com/raw/fa014623f58740b655c01f2bb726301b.png)


## 重点参数

在“鉴权信息”中可获取到使用 SDK 语音服务时所需要的参数 AppID 以及权限密钥。
![](https://main.qcloudimg.com/raw/a51de920cec5e748e3fb9b6b42a02a7c.png)

>?
>
>- 此模块中的权限密钥将会作为参数使用到 SDK 接入过程中。 
>- 页面修改密钥后，15分钟 - 1小时内生效，不建议频繁更换。
>- 只有创建游戏的账号、主账号、全局协作者可以操作【重置密钥】。
>- 鉴权详细使用请参考 [鉴权密钥](https://intl.cloud.tencent.com/document/product/607/12218)

使用 Demo 需要在 Demo 中在相应界面将腾讯云测试账号 AppID 更换为您在控制台获取的 AppID，并需要在 AVChatViewController 的 GetAuthBuffer 函数中修改实时语音的权限密钥。


## API 文档

您可根据所使用的平台或者引擎参考以下文档进行接入：

Unity 相关文档：
[工程配置文档](https://intl.cloud.tencent.com/document/product/607/10783)
[接口文档](https://intl.cloud.tencent.com/document/product/607/15228)

Unreal Engine 相关文档：
[工程配置文档](https://intl.cloud.tencent.com/document/product/607/17025)
[接口文档](https://intl.cloud.tencent.com/document/product/607/15231)

Cocos2D 相关文档：
[工程配置文档](https://intl.cloud.tencent.com/document/product/607/15216)
[接口文档](https://intl.cloud.tencent.com/document/product/607/15218)

Windows 相关文档：
[工程配置文档](https://intl.cloud.tencent.com/document/product/607/19068)
[接口文档](https://intl.cloud.tencent.com/document/product/607/15232)

iOS 相关文档：
[工程配置文档](https://intl.cloud.tencent.com/document/product/607/15219)
[接口文档](https://intl.cloud.tencent.com/document/product/607/15221)

Android 相关文档：
[工程配置文档](https://intl.cloud.tencent.com/document/product/607/15203)
[接口文档](https://intl.cloud.tencent.com/document/product/607/15210)

Mac 相关文档：
[工程配置文档](https://intl.cloud.tencent.com/document/product/607/18617)
[接口文档](https://intl.cloud.tencent.com/document/product/607/18739)

H5 相关文档：
[工程配置文档](https://intl.cloud.tencent.com/document/product/607/30261)
[接口文档](https://intl.cloud.tencent.com/document/product/607/30263)

<span id="test"></span>

## 标签管理

在 [新建应用](#test1) 时需要进行标签添加，具体操作步骤如下：

1. 在新建应用的应用信息页面，单击【[标签管理](https://console.cloud.tencent.com/tag/taglist)】进入标签列表页。
   ![](https://main.qcloudimg.com/raw/859fdef317b03d96149252ea8a27ee4e.png)
2. 单击【新建】进入“添加标签”页面，填写相关信息。
   ![](https://main.qcloudimg.com/raw/2e09f0b203819f57908ce834c7c5939f.png)
3. 单击【确定】即可创建标签成功。
