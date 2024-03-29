## 操作场景
服务端视频上传是指 App 后台将视频上传到云点播平台，本文将为您介绍如何使用服务端 API 上传视频。

## 前提条件

#### 1. 开通服务

开通云点播服务，详细请参见 [购买指引](https://intl.cloud.tencent.com/document/product/266/39506)。

#### 2. 获取云 API 密钥

获取调用服务端 API 所需的安全凭证，即 SecretId 和 SecretKey，具体步骤如下：
1. 登录控制台，选择【云产品】>【访问管理】>[【API密钥管理】](https://console.cloud.tencent.com/cam/capi)，进入“API 密钥管理”页面。
2. 获取云 API 密钥。如果您尚未创建密钥，则单击【新建密钥】即可创建一对 SecretId 和 SecretKey。

## 操作步骤
### 1. 发起上传

发起上传的方式分别为：通过 SDK 发起上传、通过 API 发起上传。

#### 通过 SDK 发起上传

为了方便用户开发端上传功能，云点播提供基于多语言平台 SDK，每种语言的 SDK 均包含相应 Demo，详情请参见：
- [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916)
- [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)
- [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918)
- [Go SDK](https://intl.cloud.tencent.com/document/product/266/33919)
- [C# SDK](https://intl.cloud.tencent.com/document/product/266/33915)

#### 通过 API 发起上传

如果云点播提供的上传 SDK 没有涵盖 App 后台所使用的语言，则 App 后台需要自行调用云点播的服务端 API 进行视频上传（这种方式较为复杂，不推荐），基于 API 上传的业务流程图如下：
![](https://main.qcloudimg.com/raw/005ec15acf74e0a428e8d328ffd2da2f.png)
相比 SDK 方式的上传，基于 API 方式的上传需要自行实现申请上传和上传文件等步骤。而上传文件也没有 SDK 的方式方便，对于大文件需要自己做分片上传等逻辑。详情请参见：

- [服务端 API - 申请上传](https://intl.cloud.tencent.com/document/product/266/34120)
- [服务端 API - 上传文件](https://intl.cloud.tencent.com/document/product/266/33913)
- [服务端 API - 确认上传](https://intl.cloud.tencent.com/document/product/266/34119)

#### 高级功能

- **上传时指定任务流**
如果开发者需要在视频上传完成后自动发起 [视频处理任务流](https://intl.cloud.tencent.com/document/product/266/33931)（例如转码、截图等），可以在调用服务端 API [申请上传](https://intl.cloud.tencent.com/document/product/266/34120) 时通过 `Procedure` 参数来实现。参数值为任务流模板名，云点播支持 [创建任务流模板](https://intl.cloud.tencent.com/document/product/266/14058) 并为模板命名。发起任务流时，可以用任务流模板名来表示要发起的任务，云点播提供的多语言 SDK 都支持指定任务流参数，详情请参见：
	- [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [Node.js SDKSDK](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
- **上传时指定存储地域**
云点播默认提供的存储地域设置在新加坡，如果需要存储到其他区域，可以在控制台上自助添加其他存储地域，详情请参见 [上传存储设置](https://intl.cloud.tencent.com/document/product/266/18874)。设置完成后调用服务端 API [申请上传](https://intl.cloud.tencent.com/document/product/266/34120) 时通过`StorageRegion`参数来实现，参数值为存储地域的 [英文简称](https://intl.cloud.tencent.com/document/product/266/9760)。云点播提供的多语言 SDK 都支持上传时指定存储地域，详情请参见：
	- [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [Node.js SDKSDK](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	
### 2. 事件通知

视频上传完成之后，云点播会给 App 后台发起 [事件通知 - 视频上传完成](https://intl.cloud.tencent.com/document/product/266/33950)，App 后台可通过该事件感知到视频上传行为。如果要接收事件通知，则 App 需要到 [控制台 - 回调设置](https://console.cloud.tencent.com/vod/callback) 开启事件通知。[事件通知 - 视频上传完成](https://intl.cloud.tencent.com/document/product/266/33950) 主要包含如下信息：
- 新视频文件的 FileId 和 URL。
- 云点播支持在视频上传时指定透传字段，事件完成将透传字段通知到 App 后台。在事件通知中有如下字段：
	- `SourceType`：该字段被腾讯云固定成 `ServerUpload`，表示上传来源为服务端上传。
	- `SourceContext`：用户自定义透传字段，App 后台在派发签名时指定的透传内容，对应签名中的`sourceContext`参数。
- 云点播支持在视频上传完成时自动发起视频处理，如果上传时指定了 [视频处理任务流](https://intl.cloud.tencent.com/document/product/266/33931)，则在事件通知内容中也会携带任务 ID，即事件通知中的`data.procedureTaskId`字段。

更多信息请参见：
- [任务管理与事件通知](https://intl.cloud.tencent.com/document/product/266/33931)
- [事件通知 - 视频上传完成](https://intl.cloud.tencent.com/document/product/266/33950)



