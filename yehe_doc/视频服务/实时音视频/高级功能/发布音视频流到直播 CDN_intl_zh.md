本文将介绍如何将 TRTC 房间中的音视频流发布（也称作“转推”）到直播CDN上，用于兼容常规的直播播放器进行观看。

## 发布当前用户的音视频流到直播CDN

![](https://qcloudimg.tencent-cloud.cn/raw/f1df9ddcf6fbf206cb6e6b29af88ff31.png)
### 功能介绍

您可以使用 TRTCCloud 提供的接口 **startPublishMediaStream** 将房间中当前用户的音视频流发布到直播 CDN 上（“发布到 CDN” 也被常称为“转推到CDN”）。
在这个过程中，TRTC 的云端服务器不会对音视频数据进行二次的转码加工，而是直接将音视频数据直接导入到直播 CDN 服务器上，因此整个过程所产生的费用是最低的。
但房间中的每一个音视频用户都需要有一条 CDN 上的直播流与之对应，因此如果房间中有多个用户的音视频流，就需要观众端使用多个直播播放器进行观看，且多条CDN直播流之间的播放进度可能相差很大。

### 操作指引
您可以按照如下指引将房间中当前用户的音视频流发布到直播 CDN 上。
1. 创建 TRTCPublishTarget 对象，并指定 TRTCPublishTarget 对象中的 mode 参数为 `TRTCPublishBigStreamToCdn` 或者 `TRTCPublishSubStreamToCdn`，其中前者是指发布当前用户的主路画面（一般是摄像头），后者是指发布当前用户的辅路画面（一般是屏幕分享）。
2. 指定 TRTCPublishTarget 对象中的 cdnUrlList 参数为一个或者多个 CDN 推流地址（标准的 CDN 推流地址一般以 `rtmp://` 作为 URL 的前缀）。如果您指定的 url 是腾讯云的直播 CDN 推流地址，需要将 isInternalLine 设置为 true，否则请将其设置为 false。
3. 因为该模式下不涉及转码服务，所以请在调用接口时保持 `TRTCStreamEncoderParam` 和 `TRTCStreamMixingConfig` 两个参数为空。
4. 调用 startPublishMediaStream 接口，并通过 onStartPublishMediaStream 监听本地 API 调用是否成功，如果成功 onStartPublishMediaStream 中的 taskId 会返回一个不为空字符串。
5. 如果您需要停止发布动作，只需要调用 stopPublishMediaStream 并传入之前通过 onStartPublishMediaStream 获得 taskId 即可。

### 参考代码

如下这段代码的功能是发布当前用户的音视频流到直播CDN：

<dx-codeblock>
::: Java
```
// 发布当前用户的音视频流到直播CDN
TRTCCloudDef.TRTCPublishTarget target = new TRTCCloudDef.TRTCPublishTarget();
target.mode = TRTC_PublishBigStream_ToCdn;

TRTCCloudDef.TRTCPublishCdnUrl cdnUrl= new TRTCCloudDef.TRTCPublishCdnUrl();
cdnUrl.rtmpUrl = "rtmp://tencent/live/bestnews";
cdnUrl.isInternalLine = true;
target.cdnUrlList.add(cdnUrl);

mTRTCCloud.startPublishMediaStream(target, null, null);
```
:::
::: ObjC
```
// 发布当前用户的音视频流到直播CDN
TRTCPublishTarget* target = [[TRTCPublishTarget alloc] init];
target.mode = TRTCPublishBigStreamToCdn;

TRTCPublishCdnUrl* cdnUrl = [[TRTCPublishCdnUrl alloc] init];
cdnUrl.rtmpUrl = @"rtmp://tencent/live/bestnews";
cdnUrl.isInternalLine = YES;

NSMutableArray* cdnUrlList = [NSMutableArray new];
[cdnUrlList addObject:cdnUrl];
target.cdnUrlList = cdnUrlList;

[_trtcCloud startPublishMediaStream:target encoderParam:nil mixingConfig:nil];
```
:::
::: C++
```
// 发布当前用户的音视频流到直播CDN
TRTCPublishTarget target;
target.mode = TRTCPublishMode::TRTCPublishBigStreamToCdn;

TRTCPublishCdnUrl* cdn_url_list = new TRTCPublishCdnUrl[1];
cdn_url_list[0].rtmpUrl = "rtmp://tencent/live/bestnews";
cdn_url_list[0].isInternalLine = true;

target.cdnUrlList = cdn_url_list;
target.cdnUrlListSize = 1;

trtc->startPublishMediaStream(&target, nullptr, nullptr);
delete[] cdn_url_list;
```
:::
</dx-codeblock>


## 发布混合后的音视频流到直播CDN

![](https://qcloudimg.tencent-cloud.cn/raw/fa00298505bb8284bb5224b65cff4c6a.png)

### 功能介绍
如果您希望将 TRTC 房间中多个用户的音视频流混合成一路，并将混合后的音视频流发布到直播 CDN 上，可以调用 **startPublishMediaStream** 接口并同时指定 `TRTCStreamEncoderParam` 和 `TRTCStreamMixingConfig` 两个参数对混流和转码的细节进行控制。

由于 TRTC 中的多路音视频流需要先在云端进行解码，然后按照您指定的混流参数（`TRTCStreamMixingConfig`）进行混合，最终再通过您指定的参数（`TRTCStreamEncoderParam`）进行二次编码，最终才能合成一路音视频流并发布到直播 CDN 上，因此该模式下的转推服务需要额外的[转码费用](https://cloud.tencent.com/document/product/647/49446)。

### 操作指引
您可以按照如下指引将房间中多个用户的音视频流混合并发布到直播 CDN 上。
1. 创建 TRTCPublishTarget 对象，并指定 TRTCPublishTarget 中的 mode 参数为 `TRTCPublishMixStreamToCdn` 。
2. 指定 TRTCPublishTarget 对象中的 cdnUrlList 参数为一个或者多个 CDN 推流地址（标准的 CDN 推流地址一般以 `rtmp://` 作为 URL 的前缀）。如果您指定的 url 是腾讯云的直播 CDN 推流地址，需要将 isInternalLine 设置为 true，否则请将其设置为 false。
3. 通过参数 `TRTCStreamEncoderParam` 设置转码后的音视频流的编码参数：
**视频编码参数：**需要您指定混合后画面的分辨率、帧率、码率和编码的 GOP 大小，其中 GOP 推荐设置为 3s 即可，FPS 推荐设置为 15，码率和分辨率有一定的映射关系，如下表格列出了几种常用的分辨率以及其对应的推荐码率。
**音频编码参数：**需要您指定混合后音频的编码格式、编码码率、采样率和声道数。这一步首先需要您先确认一下您在调用 startLocalAudio 时第二个参数 AudioQuality 所指定的音质类型，然后根据您指定的音质类型填写此处的参数。

|videoEncodedWidth | videoEncodedHeight | videoEncodedFPS |  videoEncodedGOP |  videoEncodedKbps |
|:-------:|:-----:|:-------:|:------:|:------:|
| 640   | 360	    | 15 | 3 |  800kbps |
| 960   | 540	    | 15 | 3 | 1200kbps |
| 1280 | 720	   | 15 | 3 | 1500kbps |
| 1920 | 1080   | 15 | 3 | 2500kbps |

| TRTCAudioQuality | audioEncodedSampleRate | audioEncodedChannelNum | audioEncodedKbps | audioEncodedCodecType |
|---------|---------|---------|---------|---------|
| TRTCAudioQualitySpeech | 48000 | 1 | 50 | 0 |  
| TRTCAudioQualityDefault | 48000 | 1 | 50 | 0 |  
| TRTCAudioQualityMusic | 48000 | 2 | 60 | 2 |  

4. 通过参数 `TRTCStreamMixingConfig` 设置音频混流参数和画面排版模式：
**音频混流参数（audioMixUserList）**：默认情况下填空值即可，代表会混合房间中的所有音频，如果您只希望混合方面中某几个用户的声音，才需要指定该参数。
**画面布局参数（videoLayoutList）**：画面布局是由一个数组所定义的，数组中的每一个 TRTCVideoLayout 对象都代表了一块区域的位置、大小、背景颜色等等。如果您指定了 TRTCVideoLayout 中的 **fixedVideoUser** 字段，意味着这个 layout 对象所定义的区域被固定用来显示某个用户的画面。您也可以将 fixedVideoUser 设置为 null，这意味着您只是指定了该区域会有视频画面，但画面中的用户具体是谁是不确定的，交由 TRTC 混流服务器根据一定的规则来决定。

> **案例一：四个用户的画面被混合在了同一个画面中，我们还使用了一张图片作为背景画布**
> - layout1：定义了用户 jerry 的摄像头画面的大小和位置，画面大小为 640x480，位置在画面的中上部。
> - layout2、 layout3、 layout4：均没有指定具体的用户 Id，因此 TRTC 会根据一定的规则选择房间中 3 路用户的画面安置在这三个位置。
![](https://qcloudimg.tencent-cloud.cn/raw/6530f7a07ef88f22ec9798d41f646b63.png) <br>

> **案例二：四位用户的摄像头画面和一路屏幕分享的画面被混合在了同一个画面中**
> - layout1: 定义了用户 jerry 的屏幕分享画面的大小和位置，画面大小为 1280x720，填充模式为可能有黑边的 Fit 模式，背景填充色为黑色，位置在画面的左侧。
> - layout2: 定义了用户 jerry 的摄像头画面的大小和位置，画面大小为 300x200，填充模式为 Fill 模式，位置在画面的右上角。
> - layout3、layout4、layout5：均没有指定具体的用户 Id，因此 TRTC 会根据一定的规则选择房间中 3 路用户的画面安置在这三个位置。
![](https://qcloudimg.tencent-cloud.cn/raw/0cd5b07fb3e03e6a742f9c396c6ea241.png)

5. 调用 startPublishMediaStream 接口，并通过 onStartPublishMediaStream 监听本地 API 调用是否成功，如果成功 onStartPublishMediaStream 中的 taskId 会返回一个不为空字符串。
6. 如果您需要变更混流参数，比如想要调整多个画面的排版模式，您只需要通过第六步中的 taskId 调用 updatePublishMediaStream API 并传递新的 TRTCStreamMixingConfig 参数即可。TRTCStreamEncoderParam 不建议您在转推过程中进行变更，这会影响到 CDN 播放器的稳定性。
7. 如果您需要停止发布动作，只需要调用 stopPublishMediaStream 并传入之前通过 onStartPublishMediaStream 获得 taskId 即可。

### 参考代码
如下这段代码的功能是将房间中多个用户的音视频流混合并发布到直播 CDN 上：

<dx-codeblock>
::: Java
```
// 指定发布模式为 TRTC_PublishMixedStream_ToCdn
TRTCCloudDef.TRTCPublishTarget target = new TRTCCloudDef.TRTCPublishTarget();
target.mode = TRTC_PublishMixedStream_ToCdn;

// 指定发布的 CDN 推流地址
TRTCCloudDef.TRTCPublishCdnUrl cdnUrl= new TRTCCloudDef.TRTCPublishCdnUrl();
cdnUrl.rtmpUrl = "rtmp://tencent/live/bestnews";
cdnUrl.isInternalLine = true;
target.cdnUrlList.add(cdnUrl);


// 设置混合后的音视频流的二次编码参数
TRTCCloudDef.TRTCStreamEncoderParam encoderParam 
    = new TRTCCloudDef.TRTCStreamEncoderParam();
encoderParam.videoEncodedWidth = 1280;
encoderParam.videoEncodedHeight = 720;
encoderParam.videoEncodedFPS = 15;
encoderParam.videoEncodedGOP = 3;
encoderParam.videoEncodedKbps = 1000;
encoderParam.audioEncodedSampleRate = 48000;
encoderParam.audioEncodedChannelNum = 1;
encoderParam.audioEncodedKbps = 50;
encoderParam.audioEncodedCodecType = 0;

// 设置画面的布局参数
TRTCCloudDef.TRTCStreamMixingConfig mixingConfig =
      new TRTCCloudDef.TRTCStreamMixingConfig();
TRTCCloudDef.TRTCVideoLayout layout1 = new TRTCCloudDef.TRTCVideoLayout();
layout1.zOrder = 0;
layout1.x = 0;
layout1.y = 0;
layout1.width = 720;
layout1.height = 1280;
layout1.fixedVideoStreamType = TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_SUB;
layout1.fixedVideoUser.intRoomId = 1234;    
layout1.fixedVideoUser.userId = "mike"; 

TRTCCloudDef.TRTCVideoLayout layout2 = new TRTCCloudDef.TRTCVideoLayout();
layout2.zOrder = 0;
layout2.x = 1300;
layout2.y = 0;
layout2.width = 300;
layout2.height = 200;
layout2.fixedVideoStreamType = TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG;
layout2.fixedVideoUser.intRoomId = 1234;    
layout2.fixedVideoUser.userId = "mike"; 

TRTCCloudDef.TRTCVideoLayout layout3 = new TRTCCloudDef.TRTCVideoLayout();
layout3.zOrder = 0;
layout3.x = 1300;
layout3.y = 220;
layout3.width = 300;
layout3.height = 200;
layout3.fixedVideoStreamType = TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_SUB;
layout3.fixedVideoUser = null;

mixingConfig.videoLayoutList.add(layout1);
mixingConfig.videoLayoutList.add(layout2);
mixingConfig.videoLayoutList.add(layout3);
mixingConfig.audioMixUserList = null;

// 发起混流
mTRTCCloud.startPublishMediaStream(target, encoderParam, mixingConfig);
```
:::
::: ObjC
```
// 指定发布模式为 TRTCPublishMixStreamToCdn
TRTCPublishTarget* target = [[TRTCPublishTarget alloc] init];
target.mode = TRTCPublishMixStreamToCdn;

// 指定发布的 CDN 推流地址
TRTCPublishCdnUrl* cdnUrl = [[TRTCPublishCdnUrl alloc] init];
cdnUrl.rtmpUrl = @"rtmp://tencent/live/bestnews";
cdnUrl.isInternalLine = YES;

NSMutableArray* cdnUrlList = [NSMutableArray new];
[cdnUrlList addObject:cdnUrl];
target.cdnUrlList = cdnUrlList;

// 设置混合后的音视频流的二次编码参数
TRTCStreamEncoderParam* encoderParam = [[TRTCStreamEncoderParam alloc] init];
encoderParam.videoEncodedWidth = 1280;
encoderParam.videoEncodedHeight = 720;
encoderParam.videoEncodedFPS = 15;
encoderParam.videoEncodedGOP = 3;
encoderParam.videoEncodedKbps = 1000;
encoderParam.audioEncodedSampleRate = 48000;
encoderParam.audioEncodedChannelNum = 1;
encoderParam.audioEncodedKbps = 50;
encoderParam.audioEncodedCodecType = 0;

// 设置画面的布局参数
TRTCStreamMixingConfig* config = [[TRTCStreamMixingConfig alloc] init];
NSMutableArray* videoLayoutList = [NSMutableArray new];
TRTCVideoLayout* layout1 = [[TRTCVideoLayout alloc] init];
layout1.zOrder = 0;
layout1.rect = CGRectMake(0, 0, 720, 1280);
layout1.fixedVideoStreamType = TRTCVideoStreamTypeSub;
layout1.fixedVideoUser.intRoomId = 1234;
layout1.fixedVideoUser.userId = @"mike";  

TRTCVideoLayout* layout2 = [[TRTCVideoLayout alloc] init];
layout2.zOrder = 0;
layout2.rect = CGRectMake(1300, 0, 300, 200);
layout2.fixedVideoStreamType = TRTCVideoStreamTypeBig;
layout2.fixedVideoUser.intRoomId = 1234;
layout2.fixedVideoUser.userId = @"mike"; 

TRTCVideoLayout* layout3 = [[TRTCVideoLayout alloc] init];
layout3.zOrder = 0;
layout3.rect = CGRectMake(1300, 220, 300, 200);
layout3.fixedVideoStreamType = TRTCVideoStreamTypeSub;
layout3.fixedVideoUser = nil;

[videoLayoutList addObject:layout1];
[videoLayoutList addObject:layout2];
[videoLayoutList addObject:layout3];
config.videoLayoutList = videoLayoutList;
config.audioMixUserList = nil;

// 发起混流
[_trtcCloud startPublishMediaStream:target encoderParam:encoderParam mixingConfig:config];
```
:::
::: C++
```
// 指定发布模式为 TRTCPublishMixStreamToCdn
TRTCPublishTarget target;
target.mode = TRTCPublishMode::TRTCPublishMixStreamToCdn;

// 指定发布的 CDN 推流地址
TRTCPublishCdnUrl* cdn_url = new TRTCPublishCdnUrl[1];
cdn_url[0].rtmpUrl = "rtmp://tencent/live/bestnews";
cdn_url[0].isInternalLine = true;
target.cdnUrlList = cdn_url;
target.cdnUrlListSize = 1;

// 设置混合后的音视频流的二次编码参数
TRTCStreamEncoderParam encoder_param;
encoder_param.videoEncodedWidth = 1280;
encoder_param.videoEncodedHeight = 720;
encoder_param.videoEncodedFPS = 15;
encoder_param.videoEncodedGOP = 3;
encoder_param.videoEncodedKbps = 1000;
encoder_param.audioEncodedSampleRate = 48000;
encoder_param.audioEncodedChannelNum = 1;
encoder_param.audioEncodedKbps = 50;
encoder_param.audioEncodedCodecType = 0;

// 设置画面的布局参数
TRTCStreamMixingConfig config;
TRTCVideoLayout* video_layout_list = new TRTCVideoLayout[3];

TRTCUser* fixedVideoUser0 = new TRTCUser();
fixedVideoUser0->intRoomId = 1234;
fixedVideoUser0->userId = "mike"; 
video_layout_list[0].zOrder = 0;
video_layout_list[0].rect.left = 0;
video_layout_list[0].rect.top = 0;
video_layout_list[0].rect.right = 720;
video_layout_list[0].rect.bottom = 1280;
video_layout_list[0].fixedVideoStreamType =
      TRTCVideoStreamType::TRTCVideoStreamTypeSub;
video_layout_list[0].fixedVideoUser = fixedVideoUser0;  

TRTCUser* fixedVideoUser1 = new TRTCUser();
fixedVideoUser1->intRoomId = 1234;
fixedVideoUser1->userId = "mike"; 
video_layout_list[1].zOrder = 0;
video_layout_list[1].rect.left = 1300;
video_layout_list[1].rect.top = 0;
video_layout_list[1].rect.right = 300;
video_layout_list[1].rect.bottom = 200;
video_layout_list[1].fixedVideoStreamType =
      TRTCVideoStreamType::TRTCVideoStreamTypeBig;
video_layout_list[1].fixedVideoUser = fixedVideoUser1;

video_layout_list[2].zOrder = 0;
video_layout_list[2].rect.left = 1300;
video_layout_list[2].rect.top = 220;
video_layout_list[2].rect.right = 300;
video_layout_list[2].rect.bottom = 200;
video_layout_list[2].fixedVideoStreamType =
      TRTCVideoStreamType::TRTCVideoStreamTypeSub;
video_layout_list[2].fixedVideoUser = nullptr;

config.videoLayoutList = video_layout_list;
config.videoLayoutListSize = 3;
config.audioMixUserList = nullptr;

// 发起混流
trtc->startPublishMediaStream(&target, &encoder_param, &config);
delete fixedVideoUser0;
delete fixedVideoUser1;
delete[] video_layout_list;
```
:::
</dx-codeblock>

# 常见问题

1. 能否监听 CDN 流的当前状态，状态异常时该如何处理？
答：可通过监听 `onCdnStreamStateChanged` 回调获取最新的后台任务状态更新回调。更多细节可参考 API 文档。

2. 如何从单路转推切换到混流转推，是否需要手动停止再重新创建转推任务？
答：可以从单路推流任务直接切换到混流任务，只需对单路推流任务 `taskid` 发起 `updatePublishMediaStream` 推流任务变更即可。但是为了确保推流链接稳定，从单路推流切换到混流推流无法切换到纯音频或者纯视频模式。单路推流默认是音视频模式，切换后的混流也需要是音视频模式。

3. 如何实现纯视频混流？
答：配置混流设置时，`TRTCStreamEncodeParam` 里音频相关参数不要设置且 `TRTCStreamMixingConfig` 里 `audioMixUserList` 设置为空。

4. 可以给混流画面添加水印吗？
答：可以，可通过 `TRTCStreamMixingConfig` 的 `watermarkList` 进行设置。更多细节可参考 API 文档。

5. 可以混流屏幕分享内容么，我们是做教培的，需要混流转推老师的屏幕分享画面？
答：可以的。建议您使用辅路推送屏幕分享画面，然后发起将老师的摄像头画面与屏幕分享画面配置到同一个混流任务内。设置混流辅路时只需配置 `TRTCVideoLayout` 的 `fixedVideoStreamType` 为 `TRTCVideoStreamTypeSub` 即可。

6. 预设排版模式下，音频流的混合时怎么确定的？
答：使用预设排版模式的时候，混流里的音频将会从当前房间内所有上行音频里选取最多 16 路音频进行混合。

## 相关费用
### 费用的计算
云端混流转码需要对输入 MCU 集群的音视频流进行解码后重新编码输出，将产生额外的服务成本，因此 TRTC 将向使用 MCU 集群进行云端混流转码的用户收取额外的增值费用。云端混流转码费用根据转码输入的分辨率大小和转码时长进行计费，转推至 CDN 则根据月峰值带宽进行计费。详情请参见 [混流转推计费说明](https://intl.cloud.tencent.com/zh/document/product/647/47631)。

### 费用的节约
基于客户端 SDK API 混流方案下，要停止后端混流任务，需要满足如下条件之一：
- 发起混流任务（即调用 `startPublishMediaStream`）的主播退出了房间
- 调用 `stopPublishMediaStream` 主动停止混流

在其他情况下，TRTC 云端都将会尽力持续保持混流状态。因此，为避免产生预期之外的混流费用，请在您不需要混流的时候尽早通过上述方法结束云端混流。
