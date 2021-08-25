
## 快速了解移动直播 SDK

- [产品方案及架构说明](https://intl.cloud.tencent.com/document/product/1071/38146)
- [互动直播解决方案支持](https://intl.cloud.tencent.com/document/product/1071/41884)
- [常用基本概念](https://intl.cloud.tencent.com/document/product/1071/41882)
- [功能适用场景](https://intl.cloud.tencent.com/document/product/1071/41883)



## 计费模式

移动直播 SDK 的费用主要由以下部分组成： 

<table>
<tr><th>费用说明</th><th>相关文档</th></tr>
<tr>
<td>移动直播 SDK 的使用授权费用</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1071/38114">移动直播 License</a></td>
</tr><tr>
<td rowspan=3>对接使用其他腾讯云服务时产生的费用</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2819">云直播服务</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34349">即时通信服务</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/266/2838">云点播服务</a></td>
</tr>
<tr>
</tbody></table>

> ?  使用移动直播 SDK 之前，您需要开通 [云直播服务]( https://intl.cloud.tencent.com/document/product/267 )。




## 开发支持

### 体验 Demo
移动直播 SDK 提供了[腾讯云工具包 App ](https://intl.cloud.tencent.com/document/product/1071/38147)进行体验。



### 获取 License
移动直播 SDK License 主要用于解锁对应的移动直播 SDK 包在 iOS 和 Android 上的使用权限，具体获取方式请参见：
-  [获取测试版 License](https://intl.cloud.tencent.com/document/product/1071/38546#applying-for-a-trial-license) 
-  [获取正式版 License](https://intl.cloud.tencent.com/document/product/1071/38546#purchasing-an-official-license) 


> ? 若您需了解各版本 SDK 及对应的授权 License 关系说明，具体请参见 [SDK 与授权 License 对应关系](https://intl.cloud.tencent.com/document/product/1071/38149)。



### 下载 SDK

移动直播提供3个 SDK 版本，分别是**基础版 SDK**、**专业版 SDK** 和**企业版 SDK**，可通过移动直播 SDK License 使用相应的直播功能。 

| 版本类型                                                     | 说明                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [直播基础版（Smart）](https://intl.cloud.tencent.com/document/product/1071/38150#Smart) | 通过移动直播的基础版 License ，可使用直播推流、直播播放和基础美颜（美白、磨皮等）功能。 |
| [专业版（Professional）](https://intl.cloud.tencent.com/document/product/1071/38150) | 多个音视频产品的合集，除了增加了对快直播的支持，其他功能上和直播基础版的没有区别，主要是为了解决同时集成多个音视频产品时的符号冲突问题，通过移动直播的基础版 License 可使用直播推流相关功能，其他产品功能需要开通对应服务。 |

>? 若您需了解各版本 SDK 支持功能说明，具体请参见 [SDK 功能列表](https://intl.cloud.tencent.com/document/product/1071/38149)。


## 功能实践

| 若您需要                                                     | 请您阅读                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 将移动直播 SDK 集成到您的项目中                              | [SDK 集成](https://intl.cloud.tencent.com/document/product/1071/38155) |
| 将采集到的摄像头画面及麦克风声音，进行编码后推送到云直播平台中 | [摄像头推流](https://intl.cloud.tencent.com/document/product/1071/38157) |
| 将主播的手机画面作为直播源，并叠加摄像头预览进行直播         | [录屏推流](https://intl.cloud.tencent.com/document/product/1071/41878) |
| 将实时推送的直播画面通过播放端进行播放                       | [直播拉流](https://intl.cloud.tencent.com/document/product/1071/38159) |
| 通过使用 Web 超级播放器 TCPlayerLite 解决手机浏览器和 PC 浏览器上音视频流播放问题 | Web（H5）播放器 |
| 创建直播间并实现连麦互动功能                                 | [连麦互动](https://intl.cloud.tencent.com/document/product/1071/39888) |
| 设定推流画面质量                                             | [设定画面质量](https://intl.cloud.tencent.com/document/product/1071/41861) |
| 监控直播推流和播放的状态数据变化                             | SDK 指标监控 |
| 将整个直播过程录制并存储                                 | [录制和回看](https://intl.cloud.tencent.com/document/product/1071/41868) |
|使用更低延迟的播放 |  [快直播拉流](https://intl.cloud.tencent.com/document/product/1071/41875)|

> ?
>- 若您需了解各功能接口具体说明，请参见 [iOS API 概览]( https://intl.cloud.tencent.com/document/product/1071/41666 )，[Android API 概览](https://intl.cloud.tencent.com/document/product/1071/41679) 。
>- 若您使用过程中发现报错信息，可根据 [错误码](https://intl.cloud.tencent.com/document/product/1071/41678) 进行问题排查。



## 新手常见问题

-   [支持哪些推流协议？](https://intl.cloud.tencent.com/document/product/1071/39477) 
-   [直播的在线人数是否有上限？](https://intl.cloud.tencent.com/document/product/1071/39695) 
-   [直播录制后，如何获取录制文件？](https://intl.cloud.tencent.com/document/product/1071/39695) 
-   [移动直播 License 是必须购买的吗？](https://intl.cloud.tencent.com/document/product/1071/39476) 
-   [购买移动直播 License 可以用于小程序直播吗？](https://intl.cloud.tencent.com/document/product/1071/39476) 
-   [如何降低直播延迟？](https://cloud.tencent.com/document/product/454/7947) 
-   [推流失败怎么办？](https://intl.cloud.tencent.com/document/product/1071/39360) 
-   [播放失败怎么办？](https://intl.cloud.tencent.com/document/product/1071/39361) 
-   [如何优化视频卡顿？](https://cloud.tencent.com/document/product/454/7946) 
-   [如何生成 UserSig 签名？](https://intl.cloud.tencent.com/document/product/1071/39471) 

> ? 更多问题，请您前往 [常见问题](https://intl.cloud.tencent.com/document/product/1071/39477) 文档查看。


## 反馈与建议

使用腾讯移动直播 SDK 产品和服务中有任何问题或建议，您可以通过以下渠道反馈：

- 如果发现产品文档的问题，如链接、内容等，您可以单击文档页右侧 【文档反馈】或选中存在问题的内容进行反馈。
- 如果遇到产品相关问题，您可 [提交工单](https://console.cloud.tencent.com/workorder/category) 寻求帮助。





