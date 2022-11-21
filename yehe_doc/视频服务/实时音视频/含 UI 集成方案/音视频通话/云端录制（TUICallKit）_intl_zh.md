本文将介绍如何开启 TUICallKit 的云端录制，方便重要通话的存档、审核等，我们提供了两个方案供您选择：[自动录制方案](#Option1) 和 [REST API 录制方案](#Option2)。

>? TUICallKit 整合有多个腾讯云基础的 PaaS 服务，其中音视频相关能力依赖于[实时音视频 TRTC](https://www.tencentcloud.com/document/product/647/35078)，因为 TUICallKit 的云端录制功能需要进入 [实时音视频控制台 ](https://console.tencentcloud.com/trtc/app)进行配置。

[](id:Option1)
## 方案一：自动录制方案（推荐）

我们推荐您使用自动录制的方案，录制不需业务方来启动和停止，由腾讯云实时音视频后台来管理录制任务，通话过程中有音视频流上行时就自动录制，**接入过程快速、简单**，您可以通过如下几步完成： 

1. 在 [实时音视频控制台 > 应用管理](https://console.tencentcloud.com/trtc/app) 找到对应 SDKAppId 的应用，进入功能配置页。

2. 在功能配置页，您可以看到云端录制配置的卡片，**启用云端录制**功能后，单击**创建全局自动录制模版**。![img](https://qcloudimg.tencent-cloud.cn/raw/8ea4cb2a816edfdc7e26816505a75eca.png)

3. 根据音视频通通话的业务场景（1v1通话、群组通话），我们推荐如下配置参数，当然您也可以根据自己的业务需求配置自定义录制模版。![img](https://qcloudimg.tencent-cloud.cn/raw/8f8a9d9d029d63fa2d70c1105630aa20.png)

>! 全局录制支持最大混流人数为 8，若您的通话人数超过8时（包括自己），最后一个用户的流无法录制。

开启全局自动录制功能后，在通话接听后且有音视频上行，就会触发自动启动录制任务，在通话结束后会自动停止录制，如果因为网络或者其他情况异常退房，我们的录制后台会根据您设置的 MaxIdleTime值（空闲等待时间，默认5s）自动停止录制任务，避免造成额外的计费损失。

4. **模版创建完成后，勾选**全局自动录制即可完成。

[](id:Option2)

## 方案二：REST API 录制方案

如果自动录制方案不满足您的业务需求，您也可以采用更加灵活的 REST API 录制方案，可以指定录制订阅房间内的主播，自定义合流布局，录制中途更新布局和订阅等，但是**需要搭配业务后台服务，接入复杂，功能强大，关键步骤如下**：

1. 在 [实时音视频控制台 > 应用管理](https://console.tencentcloud.com/trtc/app) 找到对应 SDKAppId 的应用，进入功能配置页。

2. 在功能配置页，您可以看到云端录制配置的卡片，**启用云端录制**功能，此时默认勾选**手动自定义录制**，即 REST API 模式。![img](https://qcloudimg.tencent-cloud.cn/raw/8ea4cb2a816edfdc7e26816505a75eca.png)

3. 然后您就可以调用 REST API （[CreateCloudRecording](https://www.tencentcloud.com/document/product/647/46960)）来启动云端的录制，这里建议您可以通过监听 [TUICallObserver](https://www.tencentcloud.com/document/product/647/51007) 的通知事件，在音视频通话开始的时候开启录制，以 Java 代码为例：

```java
TUICallEngine.createInstance(context).addObserver(new TUICallObserver() {
    @Override
    public void onCallBegin(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole) {
        // 通知您的业务后台，使用REST API 启动录制任务。
    }
});
```

4. 考虑到客户端有可能会存在网络差、杀进程的情况造成的通话异常挂断，所以如何结束录制，建议您可以通过订阅 TRTC 房间状态的回调（详情请参见 [监听服务端事件回调](https://www.tencentcloud.com/document/product/647/39558)），在收到 TRTC 房间状态解散的回调后，调用 REST API （[DeleteCloudRecording](https://www.tencentcloud.com/document/product/647/46959)）来停止云端的录制任务。

## 常见问题

### 1. 如何查看录制时长明细？

您可以在 [实时音视频控制台 > 云端录制](https://console.tencentcloud.com/trtc/statistics/cloud-record)查看录制的一些时长明细。

### 2. 如何查看录制的文件？

您可以登录 [云点播控制台](https://console.tencentcloud.com/vod)，在左侧导航栏选择**媒资管理，**单击列表上方的**前缀搜索**，选择**前缀搜索**，在搜索框输入关键词，录制文件命名规则如下：

- 单流录制 MP4 文件名规则： `<SdkAppId>_<RoomId>_UserId_s_<UserId>_UserId_e_<MediaId>_<Index>.mp4`
- 合流录制 MP4 文件名规则： `<SdkAppId>_<RoomId>_<Index>.mp4`