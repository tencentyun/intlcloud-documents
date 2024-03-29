## 操作场景
客户端视频上传是指 App 的最终用户将本地视频上传到云点播平台，其流程图如下。本文将为您介绍如何使用客户端上传视频。
![](https://main.qcloudimg.com/raw/b92eb9f4b61aa7f3605e3a372ace494e.png)

## 前提条件

#### 1. 开通服务

开通云点播服务。

<span id = "p3"></span>
#### 2. 获取云 API 密钥
 
获取调用服务端 API 所需的安全凭证，即 SecretId 和 SecretKey，具体步骤如下：
1. 登录控制台，选择【云产品】>【访问管理】>[【API密钥管理】](https://console.cloud.tencent.com/cam/capi)，进入“API 密钥管理”页面。
2. 获取云 API 密钥。如果您尚未创建密钥，则单击【新建密钥】即可创建一对 SecretId 和 SecretKey。


## 操作步骤
### 1. 申请上传签名
客户端需要向 App 的签名派发服务器申请上传签名，签名生成步骤请参见 [客户端上传签名](https://intl.cloud.tencent.com/document/product/266/33922)。多语言签名生成示例请参见：
- [PHP 签名示例](https://intl.cloud.tencent.com/document/product/266/33923#php-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)
- [Java 签名示例](https://intl.cloud.tencent.com/document/product/266/33923#java-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)
- [Node.js 签名示例](https://intl.cloud.tencent.com/document/product/266/33923#node.js-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)
- [C# 签名示例](https://intl.cloud.tencent.com/document/product/266/33923#c.23-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)
- [Python 签名示例](https://intl.cloud.tencent.com/document/product/266/33923#python-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)

>?
>- 由于客户端上传是直接将视频文件从客户端上传到云点播平台，无需 App 服务端中转，所以云点播必须对发起请求的客户端进行鉴权。
>- 由于 SecretKey 权限过大，App 不能将该信息泄露到客户端，否则会造成严重的安全问题，所以客户端发起上传前需要申请上传签名。


### 2. 使用 SDK 上传视频

为了方便客户端的视频上传，云点播提供多平台 SDK 方便客户接入，详细请参见：
- [Android 上传 SDK](https://intl.cloud.tencent.com/document/product/266/33925)
- [iOS 上传 SDK](https://intl.cloud.tencent.com/document/product/266/33926)
- [Web 上传 SDK](https://intl.cloud.tencent.com/document/product/266/33924)

#### 高级功能

- <span id = "p1"></span>**上传时指定任务流**
如果开发者需要在视频上传完成后自动发起 [视频处理任务流](https://intl.cloud.tencent.com/document/product/266/33931#.E4.BB.BB.E5.8A.A1.E6.B5.81)（例如转码、截图等），可以在生成 [上传签名](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0) 时通过`procedure`参数来实现，参数值为任务流模板名，云点播支持 [创建任务流模板](https://intl.cloud.tencent.com/document/product/266/14058) 并为模板命名，发起任务流时，可以用任务流模板名来表示要发起的任务。
- **上传时指定存储地域**
云点播默认提供的存储地域设置在新加坡，如果需要存储到其他区域，可以在控制台上自助添加其他存储地域，详细请参见 [上传存储设置](https://intl.cloud.tencent.com/document/product/266/18874)。设置完成后，在生成 [上传签名](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0) 时通过`storageRegion`参数来指定，参数值为存储地域的 [英文简称](https://intl.cloud.tencent.com/document/product/266/33910)。
- **上传时附带封面**
云点播允许在视频上传过程中，携带封面上传，即在上传 SDK 接口中填写相关的封面路径，详细请参见：
	- [Android 上传 SDK](https://intl.cloud.tencent.com/document/product/266/33925)
	- [iOS 上传 SDK](https://intl.cloud.tencent.com/document/product/266/33926)
	- [Web 上传 SDK](https://intl.cloud.tencent.com/document/product/266/33924)
- <span id = "p4"></span>**单次有效签名**
在视频上传过程中，App 后台派发的签名默认在有效期内是可以多次使用的。如果 App 对视频上传安全性要求很高，可以指定签名单次有效。
单次有效签名的使用方式：在 App 后台派发签名时，指定参数`oneTimeValid`为1即可，详细请参见 [客户端上传签名](https://intl.cloud.tencent.com/document/product/266/33922)。
>?单次有效签名有且只能被使用一次，该签名方式虽然更加安全，但是需要 App 做额外的异常处理，例如，上传出错时，不能简单地重复使用 SDK 上传视频，还需要重新申请上传签名。
- **断点续传**
在视频上传过程中，如果上传意外终止，用户再次上传该文件，则可以从中断处继续上传。
>?断点续传的有效时间为1天，即同一个视频上传被中断，那么1天内再次上传可以直接从断点处上传，超过1天则默认会重新上传完整视频。
>
App 开启断点续传功能的方式如下：
	- [Android 上传 SDK](https://intl.cloud.tencent.com/document/product/266/33925)，上传时设置`enableResume`字段为 True 即可。
	- [iOS 上传 SDK](https://intl.cloud.tencent.com/document/product/266/33926)，上传时设置`enableResume`字段为 True 即可。
	- [Web 上传 SDK](https://intl.cloud.tencent.com/document/product/266/33924)，内置断点续传，无需用户操作。
- **暂停/恢复/取消上传**
在视频上传过程中，云点播 SDK 允许暂停、恢复或取消上传，详细请参见：
	- [Android 上传 SDK](https://intl.cloud.tencent.com/document/product/266/33925)
	- [iOS 上传 SDK](https://intl.cloud.tencent.com/document/product/266/33926)
	- [Web 上传 SDK](https://intl.cloud.tencent.com/document/product/266/33924)

#### 常见问题 
- **如何在视频上传完成后自动发起转码**？
通过客户端上传签名中 `procedure`参数指定视频上传完成后的处理方式，详细请参见 [上传时指定任务流](#p1)。
- **App 后台收到视频上传完成的通知后，如何识别是哪个客户上传的**？
在客户端上传签名中增加`sourceContext`参数，通过该参数来携带用户身份信息，上传完成通知会将该参数传递给 App 后台，详细请参见 [事件通知](#p2)。
<span id = "p2"></span>
### 3. 事件通知

视频上传完成之后，云点播会给 App 后台发起 [事件通知 - 视频上传完成](https://intl.cloud.tencent.com/document/product/266/33950)，App 后台可通过该事件感知到视频上传行为。如果要接收事件通知，则 App 需要到 [控制台 - 回调设置](https://console.cloud.tencent.com/vod/callback) 开启事件通知。[事件通知 - 视频上传完成](https://intl.cloud.tencent.com/document/product/266/33950) 主要包含如下信息：
- 新视频文件的 FileId 和 URL。
- 云点播支持在视频上传时指定透传字段，事件完成将透传字段通知到 App 后台。在事件通知中有如下字段：
	- `SourceType`：该字段被腾讯云固定成`ServerUpload`，表示上传来源为服务端上传。
	- `SourceContext`：用户自定义透传字段，App 后台在派发签名时指定的透传内容，对应签名中的`sourceContext`参数。
- 云点播支持在视频上传完成时自动发起视频处理，如果上传时指定了 [视频处理任务流](https://intl.cloud.tencent.com/document/product/266/33931#.E4.BB.BB.E5.8A.A1.E6.B5.81)，则在事件通知内容中也会携带任务 ID，即事件通知中的`data.procedureTaskId`字段。

更多信息请参见：
- [任务管理与事件通知](https://intl.cloud.tencent.com/document/product/266/33931#.E7.BB.93.E6.9E.9C.E9.80.9A.E7.9F.A5)
- [事件通知 - 视频上传完成](https://intl.cloud.tencent.com/document/product/266/33950)





