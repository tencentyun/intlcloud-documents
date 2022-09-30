## 概述
腾讯云StreamLink提供稳定、安全的实时传输能力，满足视频供应商快速、稳定、低时延地传输视频流媒体需求。StreamLink控制台基于流维度进行管理，每一个流对应一个流的传输链路。基于StreamLink控制台可快速稳定地传输视频流媒体，同时还可对传输过程中的视频流进行全方位的质量监控。

## 查看Flow列表信息
StreamLink控制台基于Flow维度进行管理，每个Flow可以传输一路直播流，可以将这路流传到多个地域，并提供多个拉流地址。您可以在控制台[Flow Management](https://console.tencentcloud.com/mdc/flow)中管理您所有的Flow。在此页面中，您可以对 Flow 进行添加、查看、编辑、删除、启动和停止的操作。

![](https://qcloudimg.tencent-cloud.cn/raw/afd0fc995dafc79a23feb9ba2df91dae.jpg)

如图所示，**Flow**列表中会展示各个Flow的简要信息，如：
- **状态 Status**：IDLE 表示未启动，RUNNING 表示 Flow 已经启动.
- **协议 Source Protocol**：Input 的推流协议。
- **地址 Input Address**：Input 的推流地址。
只有当 Flow 停止时，才能对 Flow 进行完全的编辑操作。若没有停止 Flow， 则只能编辑白名单、删除已有的 Output 配置或者创建新的 Output 配置。