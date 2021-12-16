## 快速了解实时音视频

- [平台支持](https://intl.cloud.tencent.com/document/product/647/35078)
- [功能支持](https://intl.cloud.tencent.com/document/product/647/35428)
- [适用场景](https://intl.cloud.tencent.com/document/product/647/37713)
- [基本概念](https://intl.cloud.tencent.com/document/product/647/37714)

[](id:pay)
## 计费模式

实时音视频服务项根据服务类型划分为**基础服务**和**增值服务**两大类。 

<table>
<tr><th>服务类型</th><th>适用场景</th><th>计费说明</th></tr>
<tr>
<td rowspan="4">基础服务</td>
<td>语音互动直播</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647">语音互动直播计费说明</a></td>
</tr><tr>
<td>视频互动直播</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647">视频互动直播计费说明</a></td>
</tr><tr>
<td>语音通话</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647">语音通话计费说明</a></td>
</tr><tr>
<td>视频通话</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647">视频通话计费说明</a></td>
</tr><tr>
<td rowspan="2">增值服务</td>
<td>云端录制</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38385">云端录制计费说明</a></td>
</tr><tr>
<td>云端混流转码</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38929">云端混流转码计费说明</a></td>
</tr>
</table>




## 开发支持
[](id:demo)
### Demo 体验

实时音视频提供了 **iOS**、**Android**、**Mac OS**、**Windows**、**桌面浏览器**、**Electron**、**Flutter** 端的体验 Demo，具体详情请参见  [Demo 体验](https://intl.cloud.tencent.com/document/product/647/35076)。

[](id:sdk)
### SDK 下载

TRTC 是腾讯云 LiteAV 系列产品之一，由于 LiteAV 体系的 SDK 都使用了相同的基础模块，如果您的项目中同时集成了两款以上的 LiteAV 体系的 SDK，就会出现符号冲突（symbol duplicate）的问题。因此我们为您提供集成了不同产品能力的**精简版（TRTC）**、**专业版（Professional）**和**企业版（Enterprise）**，您可以根据实际业务需要选择不同的版本。

| 版本类型                                                     | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [精简版（TRTC）](https://intl.cloud.tencent.com/document/product/647/34615) | 仅包含 TRTC 和直播播放（TXLivePlayer）两项功能，对 App 的安装包体积增量最小，适合仅使用 TRTC 相关功能的客户 |
| [专业版（Professional）](https://intl.cloud.tencent.com/document/product/647/34615) | 包含 TRTC 在内的多个音视频相关的核心功能，包括 [移动直播（MLVB）](https://intl.cloud.tencent.com/product/mlvb) 和 [短视频（UGSV）](https://intl.cloud.tencent.com/product/ugsv) 等，由于底层模块的高度复用，集成专业版的体积增量要小于同时集成两个独立的 SDK，并且可以避免符号冲突（symbol duplicate）的困恼 |
| [企业版（Enterprise）](https://intl.cloud.tencent.com/document/product/647/34615) | 除包含专业版的所有功能以外，还集成了 AI 美颜特效组件（增值服务），支持大眼、瘦脸、美容和动效贴纸、挂件等 AI 美颜特效能力 |

> ? 各版本的差异对照，请参见 [SDK 下载](https://intl.cloud.tencent.com/document/product/647/34615)。


[](id:api)
### API 集成

- **客户端 API：**支持通过调用 SDK 接口实现功能集成，可支持平台包括 [iOS](https://intl.cloud.tencent.com/document/product/647/35119)、[Mac](https://intl.cloud.tencent.com/document/product/647/35119)、[Android](https://intl.cloud.tencent.com/document/product/647/35125)、[Windows（C++）](https://intl.cloud.tencent.com/document/product/647/35131)、[Unity](https://intl.cloud.tencent.com/document/product/647/40139)、[Web](https://intl.cloud.tencent.com/document/product/647/35143)、 [Electron](https://intl.cloud.tencent.com/document/product/647/35141)和 [Flutter](https://intl.cloud.tencent.com/document/product/647/39169)。
- **服务端 API：**支持通过调用 API 3.0 接口实现  [通话质量监控](https://intl.cloud.tencent.com/document/product/647/36754)、[混流转码](https://intl.cloud.tencent.com/document/product/647/37760)、[房间管理](https://intl.cloud.tencent.com/document/product/647/34268) 功能集成。



## 新手入门
[](id:demo_guide)
### 一分钟跑通 Demo

实时音视频控制台提供了不同平台的 Demo 源码，具体跑通方法请参见：

| 平台       | 相关文档                                                     |
| ---------- | ------------------------------------------------------------ |
| iOS 和 Mac    | [跑通 Demo（iOS&Mac）](https://intl.cloud.tencent.com/document/product/647/35086) |
| Android    | [跑通 Demo（Android）](https://intl.cloud.tencent.com/document/product/647/35084) |
| Windows    | [跑通 Demo（Windows）](https://intl.cloud.tencent.com/document/product/647/35085) |
|Web | [跑通 Demo（Web）](https://intl.cloud.tencent.com/document/product/647/35607) |
| Electron   | [跑通 Demo（Electron）](https://intl.cloud.tencent.com/document/product/647/35089) |
| Flutter | [跑通 Demo（Flutter）](https://intl.cloud.tencent.com/document/product/647/39243) |

[](id:sdk_guide)
### 一分钟集成 SDK

SDK 下载完成后，您可通过以下方式快速将 TRTC SDK 集成到您的项目中：

| 平台       | 相关文档                                                     |
| ---------- | ------------------------------------------------------------ |
| iOS        | [快速集成（iOS）](https://intl.cloud.tencent.com/document/product/647/35092) |
| Mac        | [快速集成（Mac）](https://intl.cloud.tencent.com/document/product/647/35094) |
| Android    | [快速集成（Android）](https://intl.cloud.tencent.com/document/product/647/35093) |
| Windows    | [快速集成（Windows）](https://intl.cloud.tencent.com/document/product/647/35095) |
| Web | [快速集成（Web）](https://intl.cloud.tencent.com/document/product/647/35096) |
| Electron   | [快速集成（Electron）](https://intl.cloud.tencent.com/document/product/647/35097) |
| Flutter | [快速集成（Flutter）](https://intl.cloud.tencent.com/document/product/647/35098) |

[](id:web_guide)
### 一分钟跑通 Web 直播互动组件

实时音视频提供了完整的 Web 直播互动组件体验 Demo，具体集成方法请参见 [一分钟跑通 Web 直播互动组件](https://intl.cloud.tencent.com/document/product/647/38172)。

[](id:sence)
## 场景实践

实时音视频搭配其他腾讯云产品，提供多种直播场景类型的体验 Demo。

<table>
<tr><th width="17%">场景类型</th><th>功能支持</th><th width="20%">请您阅读</th>
</tr><tr>
<td>多人视频通话</td>
<td>包括互动连麦、离线接听等相关能力</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/36065" target="_blank">实时视频通话</a></td>
</tr><tr>
<td>多人语音通话</td>
<td>包括互动连麦、离线接听等相关能力</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/36067" target="_blank">实时语音通话</a></td>
</tr><tr>
<td>互动直播</td>
<td>包括互动连麦、主播 PK、低延时观看、弹幕聊天等相关能力</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/36060" target="_blank">视频互动直播</a></td>
</tr><tr>
<td>实时互动课堂</td>
<td>包括语音、视频、屏幕分享等上课方式，还封装了老师开始问答、学生举手、老师邀请学生上台回答、结束回答等相关能力</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37278" target="_blank">实时互动课堂</a></td>
</tr><tr>
<td>多人视频会议</td>
<td>包括屏幕分享、美颜、低延时会议等相关能力</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37284" target="_blank">多人视频会议</a></td>
</tr><tr>
<td>语音聊天室</td>
<td>包括麦位管理、低延时语音互动、文字聊天等相关能力</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37287" target="_blank">语音聊天室</a></td>
</tr></table>

[](id:console)
## 控制台实践
| 如果您想通过控制台                                         | 您可以阅读                                                   |
| :--------------------------------------------------------- | :----------------------------------------------------------- |
| 查看使用 TRTC 时产生的**音视频互动**和**云端录制**用量数据 | [用量统计](https://intl.cloud.tencent.com/document/product/647/39066) |
| 使用监控仪表盘功能了解应用房间的通话质量详情               | [监控仪表盘](https://intl.cloud.tencent.com/document/product/647/39069) |
| 创建下载 Demo 应用，并能快速跑通试用                       | [快速跑通 Demo](https://intl.cloud.tencent.com/document/product/647/39073) |
| 在线生成签名 UserSig，或检验已有 UserSig 是否有效         | [UserSig 生成与校验](https://intl.cloud.tencent.com/document/product/647/39074)                |
| 创建新的应用 | [创建应用](https://intl.cloud.tencent.com/document/product/647/39077) |
| 为某个应用开启旁路推流、云端录制或高级权限控制功能         | [功能配置](https://intl.cloud.tencent.com/document/product/647/39080) |
| 为云端混流转码时所需的自定义背景图片添加图片素材           | [素材管理](https://intl.cloud.tencent.com/document/product/647/39081) |
| 结合实际业务需求，配置回调密钥和回调地址 | [回调配置](https://intl.cloud.tencent.com/document/product/647/39559) |



[](id:faq)
## 新手常见问题

-  [客户端 Native SDK 需要配置哪些端口或域名为白名单？](https://intl.cloud.tencent.com/document/product/647/35164)
-  [如何缩减 iOS/Android 安装包体积？](https://intl.cloud.tencent.com/document/product/647/35165)
-  [如何获取 UserSig 密钥？](https://intl.cloud.tencent.com/document/product/647/35166)
-  [TRTC 精简版、专业版、企业版各个版本区别？](https://intl.cloud.tencent.com/document/product/647/36057) 
-  [实时音视频 RoomID 是什么？取值区间值是多少？](https://intl.cloud.tencent.com/document/product/647/36057) 
-  [是否支持 Android 和 Web 端互通？](https://intl.cloud.tencent.com/document/product/647/37341) 
-  [桌面浏览器端 SDK 的支持哪些浏览器？](https://intl.cloud.tencent.com/document/product/647/37340) 

> ? 更多问题，建议您前往 [常见问题](https://intl.cloud.tencent.com/document/product/647/36058) 文档查看。


## 反馈与建议

使用腾讯实时音视频产品和服务中有任何问题或建议，您可以通过以下渠道反馈：

- 如果发现产品文档的问题，如链接、内容等，您可以单击文档页右侧 【文档反馈】或选中存在问题的内容进行反馈。
- 如果遇到产品相关问题，您可 [提交工单](https://console.cloud.tencent.com/workorder/category) 寻求帮助。
