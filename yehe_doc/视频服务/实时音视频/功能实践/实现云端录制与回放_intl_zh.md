## 适用场景
在远程教育、秀场直播、视频会议、远程定损、金融双录、在线医疗等应用场景中，考虑取证、质检、审核、存档和回放等需求，常需要将整个视频通话或互动直播过程录制和存储下来。

TRTC 的云端录制，可以将房间中的每一个用户的音视频流都录制成一个独立的文件：
![](https://main.qcloudimg.com/raw/7820cdafe40fabc38653bc53795412d2.png)

也可以将房间中的多路音视频先进行 [云端混流](https://intl.cloud.tencent.com/document/product/647/34618)，再将混合后的音视频流录制成一个文件：
![](https://main.qcloudimg.com/raw/2f92f978c2ca76d001891e645905e8f9.png)

## 控制台指引

<span id="open"></span>
### 开通录制服务
1. 登录 [实时音视频控制台](https://console.cloud.tencent.com/trtc)，在左侧导航栏选择【应用管理】。
2. 单击目标应用所在行的【功能配置】，进入功能配置页卡。如果您还没有创建过应用，可以单击【创建应用】，填写应用名称，单击【确定】创建一个新的应用。
3. 单击【启动云端录制】右侧的 <img src="https://main.qcloudimg.com/raw/3fc81b259baa4edf112af2f570e6d97f.png"  style="margin:0;"> ，会弹出云端录制的设置页面。

<span id="recordType"></span>
### 选择录制形式
TRTC 的云端录制服务提供了两种不同的录制形式：“全局自动录制”和“指定用户录制”：
![](https://main.qcloudimg.com/raw/d8084b7aa472b95ec21448703e4b6a49.png)

- **全局自动录制**
每一个 TRTC 房间中的每个用户的音视频上行流都会被自动录制下来，录制任务的启动和停止都是自动的，不需要您额外操心，比较简单和易用。具体的使用方法请阅读 [方案一：全局自动录制](#autoRecord)。

- **指定用户录制**
您可以指定只录制一部分用户的音视频流，这需要您通过客户端的 SDK API 或者服务端的 REST API 进行控制，需要额外的开发工作量。具体的使用方法请阅读 [方案二：指定用户录制（SDK API）](#recordSDKAPI) 和 [方案三：指定用户录制（REST API）](#recordRESTAPI)。

<span id="fileFormat"></span>
###  选择文件格式
云端录制支持 HLS、MP4、FLV 和 AAC 四种不同的文件格式，我们以表格的形式列出四种不同格式的差异和适用场景，您可以结合自身业务的需要进行选择：

<table>
<tr>
<th>参数</th>
<th>参数说明</th>
</tr>
<tr>
<td>文件类型</td>
<td>支持以下文件类型：<ul><li><b>HLS</b>：该文件类型支持绝大多数浏览器在线播放，适合视频回放场景。选择该文件类型时，支持断点续录且不限制单个文件最大时长。</li><li><b>FLV</b>：该文件类型不支持在浏览器在线播放，但该格式简单容错性好。如果无需将录制文件存储在云点播平台，可以选择该文件类型，录制完成后立刻下载录制文件并删除源文件。</li><li><b>MP4</b>：该文件类型支持在 Web 浏览器在线播放，但此格式容错率差，视频通话过程中的任何丢包都会影响最终文件的播放质量。</li><li><b>AAC</b>：如果只需录制音频，可以选择该文件类型。</li></td>
</tr>
<tr>
<td nowrap="nowrap">单个文件的最大时长（分钟）</td>
<td>根据实际业务需求设置单个视频文件的最大时长限制，超过长度限制后系统将会自动拆分视频文件。单位为分钟，取值范围5 - 120。<br>当【文件类型】设置为【HLS】时，不限制单个文件的最大时长，即该参数无效。</td>
</tr>
<tr>
<td>文件保存时长（天）</td>
<td>根据实际业务需求设置视频文件存储在云点播平台的天数。单位为天，取值范围0 - 1800，到期后文件将被点播平台自动删除且无法找回， 0表示永久存储。</td>
</tr>
<tr>
<td>续录超时时长（秒）</td>
<td>仅当【文件类型】设置为【HLS】时，该参数有效。<br>默认情况下，若通话（或直播）过程因网络波动或其他原因被打断，录制文件会被切断成多个文件。如果需要实现“一次通话（或直播）只产生一个回放链接”，可以根据实际情况设置续录超时时长，当打断间隔不超过设定的续录超时时长时，一次通话（或直播）只会生成一个文件。单位为秒，取值范围1 - 300，0表示断点后不续录。</td>
</tr>
</table>

>? 
- 在线教育类业务推荐选择 HLS 用于课程回放。
HLS 支持最长五分钟的续录，可以做到“一堂课只产生一个回放链接”，且支持绝大多数浏览器的在线观看，非常适合视频回放场景。
- 需要将录制文件自行存储时，推荐选择 FLV 格式。
由于 HLS 是由一系列小的 ts 文件组成的，在服务器之间的迁移并不方便，所以如果您是要自行存储于自建的服务器上，请选择格式简单且容错性能力好的 FLV。

<span id="storageLocation"></span>
###  选择存储位置
TRTC 云端录制文件会默认存储于腾讯云点播服务上，如果您的项目中多个业务公用一个腾讯云点播账号，可能会有录制文件隔离的需求。您可以通过腾讯云点播的“子应用”能力，将 TRTC 的录制文件与其他业务区分开。

- **什么是点播主应用和子应用？**
主应用和子应用是云点播上的一种资源划分的方式。主应用相当于云点播的主账号，子应用可以创建多个，每一个子应用相当于主账号下面的一个子账号，拥有独立的资源管理，存储区域可以跟其他的子应用相互隔离。

- **如何开启点播服务的子应用？**
您可以根据文档 [“如何开启点播子应用”](https://intl.cloud.tencent.com/document/product/266/33987) 添加新的子应用，这一步需要您跳转到点播[控制台](https://console.cloud.tencent.com/vod)中进行操作。

<span id="recordCallback"></span>
###  设置录制回调
如果您需要实时接收到新文件的 [落地通知](#callback)，可在此处填写您的服务器上用于接收录制文件的回调地址，该地址需符合 HTTP（或 HTTPS）协议。当新的录制文件生成后，腾讯云会通过该地址向您的服务器发送通知。



详细的录制回调接收和解读方案请参考文档后半部分的：[接收录制文件](#callback)。

<span id="startAndStop"></span>
## 录制控制方案
TRTC 提供了三种云端录制的控制方案，分别是“全局自动录制”、“指定用户录制（由 SDK API 控制）”和“指定用户录制（由 REST API 控制）”。对于其中的每一种方案，我们都会详细介绍：
- 如何在控制台中设定使用该方案？
- 如何开始录制任务？
- 如何结束录制任务？
- 如何将房间中的多路画面混合成一路？
- 录制下来的文件会以什么格式命名？
- 支持该种方案的平台有哪些？

<span id="autoRecord"></span>
### 方案一：全局自动录制
- **控制台中的设定**
要使用该种录制方案，请在控制台中 [选择录制形式](#recordType) 时，设定为“全局自动录制”。

- **录制任务的开始**
TRTC 房间中的每一个用户的音视频流都会被自动录制成文件，无需您的额外操作。

- **录制任务的结束**
自动停止。即每个主播在停止音视频上行后，该主播的云端录制即会自行停止。如果您在 [选择文件格式](#fileFormat) 时设置了“续录时间”，则需要等待续录时间超时后才能收到录制文件。

- **多路画面的混合**
全局自动录制模式下的云端混流有两种方案，即“服务端 REST API 方案” 和 “客户端 SDK API 方案”，两套方案请勿混合使用：
 + [服务端 REST API 混流方案](https://intl.cloud.tencent.com/document/product/647/34618#restapi)：需要由您的服务器发起 API 调用，不受客户端平台版本的限制。
 + [客户端 SDK API 混流方案](https://intl.cloud.tencent.com/document/product/647/34618#sdkapi)：可以直接在客户端发起混流，目前支持 iOS、Android、Windows、Mac 和 Electron 等平台，暂不支持微信小程序和 Web 浏览器。


- **录制文件的命名**
 + 如果主播在进房时指定了 [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 参数，则录制文件会以 `userDefineRecordId_开始时间_结束时间` 来命名；
 + 如果主播在进房时没有指定 [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 参数，但指定了 [streamId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) 参数，则录制文件会以 `streamId_开始时间_结束时间` 来命名；
 + 如果主播在进房时既没有指定 [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 参数，也没有指定 [streamId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) 参数，则录制文件会以 `sdkappid_roomid_userid_开始时间_结束时间` 来命名。
 
- **已经支持的平台**
由您的服务端控制，不受客户端平台限制。

<span id="recordSDKAPI"></span>
### 方案二：指定用户录制（SDK API）

![](https://main.qcloudimg.com/raw/e3d81ef76c64d2fb6631d98d22bfb0dc.png)

- **控制台中的设定**
要使用该种录制方案，请在控制台中 [选择录制形式](#recordType) 时，设定为“指定用户录制”。

- **录制任务的开始**
主播在进房时指定进房参数 [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCParams) 中的 [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 字段，之后该主播的上行音视频数据即会被云端录制下来，不指定该参数的主播不会触发录制任务。

```Objective-C
// 示例代码：指定录制用户 rexchang 的音视频流，文件 id 为 1001_rexchang
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // TRTC 的 SDKAppID，创建应用后可获得
param.roomId   = 1001;           // 房间号
param.userId   = @"rexchang";    // 用户名
param.userSig  = @"xxxxxxxx";    // 登录签名
param.role     = TRTCRoleAnchor; // 角色：主播
param.userDefineRecordId = @"1001_rexchang";  // 录制 ID，即指定开启该用户的录制。
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; // 请使用 LIVE 模式
```

- **录制任务的结束**
自动停止，当进房时指定 [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 参数的主播在停止音视频上行后，云端录制会自行停止。如果您在[选择文件格式](#fileFormat)时设置了“续录时间”，则需要等待续录时间超时后才能收到录制文件。

- **多路画面的混合**
您可以通过调用 SDK API  [setMixTranscodingConfig()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) 将房间中其它用户的画面和声音混合到当前用户的这一路音视频流上。关于这一部分详细介绍，可以阅读文档：[云端混流转码](https://intl.cloud.tencent.com/document/product/647/34618#.E6.96.B9.E6.A1.88.E4.B8.80.EF.BC.9A.E6.9C.8D.E5.8A.A1.E7.AB.AF-rest-api-.E6.B7.B7.E6.B5.81.E6.96.B9.E6.A1.88)。

- **录制文件的命名**
录制文件会以 `userDefineRecordId_开始时间_结束时间` 的格式来命名。

- **已经支持的平台**
支持 [iOS](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce)、[Android](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a154fa0570c3bb6a9f99fb108bda02520)、[Windows](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#a3a7a5e6144aa337752d22269d25f7cfc)、[Mac](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce)、[Electron](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html) 等终端发起录制控制，暂不支持由 Web 浏览器和微信小程序端发起控制。

<span id="recordRESTAPI"></span>
### 方案三：指定用户录制（REST  API）

![](https://main.qcloudimg.com/raw/71b4b6705cee61000660c13c2a0fe595.png)

>? TRTC 的服务端提供了一对 REST API（ [StartMCUMixTranscode](https://cloud.tencent.com/document/product/647/44270) 和 [StopMCUMixTranscode](https://cloud.tencent.com/document/product/647/44269)）用于实现云端混流、云端录制和旁路直播三个功能：
>- 云端混流：通过 `LayoutParams` 参数可以控制混流时的画面布局。
>- 云端录制：通过 `OutputParams.RecordId` 参数可以启动/关闭云端录制。
>- 旁路直播：通过 `OutputParams.StreamId` 参数可以启动/关闭 CDN 直播。

- **控制台中的设定**
要使用该种录制方案，请在控制台中 [选择录制形式](#recordType) 时，设定为“指定用户录制”。

- **录制任务的开始**
由您的服务器调用 [StartMCUMixTranscode](https://cloud.tencent.com/document/product/647/44270) ，并指定 `OutputParams.RecordId` 参数即可启动混流和录制。

```
// 代码示例：通过 REST API 启动云端混流和云端录制任务
https://trtc.tencentcloudapi.com/?Action=StartMCUMixTranscode
&SdkAppId=1400000123
&RoomId=1001
&OutputParams.RecordId=1400000123_room1001
&OutputParams.RecordAudioOnly=0
&EncodeParams.VideoWidth=1280
&EncodeParams.VideoHeight=720
&EncodeParams.VideoBitrate=1560
&EncodeParams.VideoFramerate=15
&EncodeParams.VideoGop=3
&EncodeParams.BackgroundColor=0
&EncodeParams.AudioSampleRate=48000
&EncodeParams.AudioBitrate=64
&EncodeParams.AudioChannels=2
&LayoutParams.Template=1
&<公共请求参数>
```

- **录制任务的结束**
自动停止，您也可以中途调用 StopMCUMixTranscode

- **多路画面的混合**
由您的服务器调用 StartMCUMixTranscode

- **录制文件的命名**
录制文件会以调用 StartMCUMixTranscode 时指定的 `OutputParams.RecordId` 参数来命名，命名格式为 `OutputParams.RecordId_开始时间_结束时间`。

- **已经支持的平台**
由您的服务端控制，不受客户端平台的限制。

<span id="search"></span>
## 查找录制文件
在开启录制功能以后，TRTC 系统中录制下来的文件就能在腾讯云点播服务中找到。您可以直接在云点播控制台手动查找，也可以由您的后台服务器使用 REST API 进行定时筛选：

**方式一：在点播控制台手动查找**
1. 登录 [云点播控制台](https://console.cloud.tencent.com/vod/)，在左侧导航栏选择【媒资管理】。
2. 单击列表上方的【前缀搜索】，选择【前缀搜索】，在搜索框输入关键词，例如`1400000123_1001_rexchang_main`，单击<img src="https://main.qcloudimg.com/raw/16b35c89b5efe4a7153e1cb5282006fd.png"  style="margin:0;">，将展示视频名称前缀相匹配的视频文件。
3. 您可以根据创建时间筛选所需的目标文件。

**方式二：通过点播 REST API 查找**
腾讯云点播系统提供了一系列 REST API 来管理其上的音视频文件，您可以通过 [搜索媒体信息](https://intl.cloud.tencent.com/document/product/266/34179) 这个 REST API 来查询您在点播系统上的文件。您可以通过请求参数表中的 `Text` 参数进行模糊匹配，也可以根据 `StreamId` 参数进行精准查找。
REST 请求示例：
```
https://vod.tencentcloudapi.com/?Action=SearchMedia
&StreamId=stream1001
&Sort.Field=CreateTime
&Sort.Order=Desc
&<公共请求参数>
```

<span id="callback"></span>
## 接收录制文件
除了 [查找录制文件](#search)，您还可以通过配置回调地址，让腾讯云主动把新录制文件的消息推送给您的服务器。
房间里的最后一路音视频流退出后，腾讯云会结束录制并将文件转存到云点播平台，该过程大约默认需要30秒至2分钟（若您设置了续录时间为300秒，则等待时间将在默认基础上叠加300秒）。转存完成后，腾讯云会通过您在 [设置录制回调](#recordCallback) 中设置的回调地址（HTTP/HTTPS）向您的服务器发送通知。

腾讯云会将录制和录制相关的事件都通过您设置的回调地址推送给您的服务器，回调消息示例如下图所示：
![](https://main.qcloudimg.com/raw/1a89e7058f7c806f6f867217821d1a9c.png)
您可以通过下表中的字段来确定当前回调是对应的哪一次通话（或直播）：

<table>
<tr>
<th>序号</th>
<th>字段名</th>
<th>说明</th>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/b75fdd3c8a2c0b1562ee4cb5a4ef65d1.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>event_type</td>
<td>消息类型，当 event_type 为100时，表示该回调消息为录制文件生成的消息。</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/2a495b157f03a8905e372a2516ea3a8f.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_id</td>
<td>您可以在进房时通过设置 TRTCParams 中的 <a href="http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167">streamId</a> 字段指定。</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/1cf7ec54371a5e95e2ea00bdda4d1a64.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userid</td>
<td>用户名的 Base64 编码。</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/66d50d985be81cae9698fae3ffa40f40.png" style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userdefinerecordid</td>
<td>自定义字段，您可以通过设置 TRTCParams 中的 <a href="http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce">userDefineRecordId</a> 字段指定。</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/d1cb894a93a1d69cd4215c54064eca5d.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>video_url</td>
<td>录制文件的观看地址，可以用于 <a href="#play">点播回放</a>。</td>
</tr></table>

<span id="delete"></span>
## 删除录制文件
腾讯云点播系统提供了一系列 REST API 来管理其上的音视频文件，您可以通过 删除媒体 API 删除某个指定的文件。
REST 请求示例：
```
https://vod.tencentcloudapi.com/?Action=DeleteMedia
&FileId=52858907988664150587
&<公共请求参数>
```

<span id="play"></span>
## 回放录制文件
在线教育等场景中，通常需要在直播结束后多次回放录制文件，以便充分利用教学资源。

**选择文件格式（HLS）**
在 [设置录制格式](#fileFormat) 中选择文件格式为 HLS。
HLS 支持最长5分钟的断点续录，可以做到“一场直播（或一堂课）只产生一个回放链接”，且 HLS 文件支持绝大多数浏览器在线播放，非常适合视频回放场景。

**获取点播地址（video_url）**
在 [接收录制文件](#callback) 时，可以获取回调消息中 **video_url** 字段，该字段为当前录制文件在腾讯云的点播地址。

**对接点播播放器**
根据使用平台对接点播播放器，具体操作参考如下：
- [iOS 平台](http://doc.qcloudtrtc.com/group__TXVodPlayer__ios.html)
- [Android 平台](http://doc.qcloudtrtc.com/group__TXVodPlayer__android.html)

>! 建议使用 [专业版](https://intl.cloud.tencent.com/document/product/647/34615) TRTC SDK，专业版集合了 超级播放器（Player+）、移动直播（MLVB） 等功能，由于底层模块的高度复用，集成专业版的体积增量要小于同时集成两个独立的 SDK，并且可以避免符号冲突（symbol duplicate）的困扰。
