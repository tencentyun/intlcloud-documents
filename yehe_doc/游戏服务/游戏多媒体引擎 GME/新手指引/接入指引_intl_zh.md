为方便开发者接入腾讯云游戏多媒体引擎产品，本文主要为您介绍适用于游戏多媒体引擎 SDK 的接入指引。



## 新建服务
#### 新建应用
1. 登录 [游戏多媒体引擎控制台](https://console.cloud.tencent.com/gamegme)，单击左侧菜单【服务管理】。
2. 进入服务管理页面，单击【新建应用】。


#### 填写信息
填写该页面所需信息，按照需要选择所需的服务。 
- 计费详情请参考 [产品价格](https://intl.cloud.tencent.com/document/product/607/17808) 或者咨询相关腾讯云商务工作人员。设置完成可再修改。
- 语音消息及转文本服务设置完成可再修改。

![](https://main.qcloudimg.com/raw/6a7f84cf85f38d6ee87e98feb710ba23.png)

## 设置服务
#### 查看应用
列表中的 AppID 在接入 SDK 进行开发过程中会作为参数使用。

![](https://main.qcloudimg.com/raw/90dabc58f16597ce5ef934f47d1e6707.png)


#### 设置应用
单击【设置】，进入应用信息模块，单击【修改】后可对相应信息进行修改。

![](https://main.qcloudimg.com/raw/d915147f17ca0e31fc623c022f3c608b.png)



#### 鉴权信息

- 此模块中的权限密钥会作为参数使用到 SDK 接入过程中。 
- 页面修改密钥后，15分钟 - 1小时内生效，不建议频繁更换。
- 只有创建游戏的账号、主账号、全局协作者可以操作【重置密钥】。
- 鉴权详细使用请参考 [鉴权密钥](https://main.qcloudimg.com/raw/973b60c364a7ee43537db2dbdad37494.png)


#### 开启关闭业务
在这里可以对业务及服务进行开启或者关闭。

![](https://main.qcloudimg.com/raw/90dabc58f16597ce5ef934f47d1e6707.png)



## 下载 SDK 
#### 1. 下载地址
请在 [SDK 下载指引](https://intl.cloud.tencent.com/document/product/607/18521) 下载相关 Demo 及 SDK。

#### 2. 接入准备
接入 SDK 需要使用腾讯云提供的 AppID 及相关权限密钥。即应用管理列表中的 AppID 及 应用设置中的鉴权信息模块。

更多平台相关配置请参考各平台工程配置文档。

#### 3. 官方 Demo 使用需知
Demo 中带有腾讯云测试账号，可进行功能体验，如需更换个人及公司测试账号，需要在 Demo 中在相应界面将腾讯云测试账号 AppID 更换为开发者在控制台获取的 AppID，并需要在 AVChatViewController-GetAuthBuffer 函数中修改实时语音的权限密钥。


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



## 相关文档
更多详情请参见 [运营指引](https://intl.cloud.tencent.com/document/product/607/17448)。



如有疑问请参考 [一般性问题](https://intl.cloud.tencent.com/document/product/607/30254) 和 [错误码](https://intl.cloud.tencent.com/document/product/607/15173)。




