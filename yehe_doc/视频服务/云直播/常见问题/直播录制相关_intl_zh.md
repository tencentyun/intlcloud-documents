<span id="que1"></span>
###  直播录制的原理是什么？
![img](https://main.qcloudimg.com/raw/9c9d31c6ffec97d2b8b4042b7a673cbc.jpg)

对于一条直播流，一旦开启录制，音视频数据就会被旁路到录制系统。主播的手机推上来的每一帧数据，都会被录制系统追加写入到录制文件中。

一旦直播流中断，接入层会立刻通知录制服务器将正在写入的文件落地，将其转存到点播系统中，并为其生成索引，这样您在点播系统中就会看到这个新生成的录制文件了。同时，如果您配置了录制事件通知，录制系统会将该文件的**索引 ID** 和**在线播放地址**等信息通知给您之前配置的服务器上。

但是，如果一个文件过大，在云端的转出和处理过程中就很容易出错，所以为了确保成功率，我们的单个录制文件最长不会超过120分钟，您可以通过 RecordInterval 参数指定更短的分片。

<span id="que2"></span>
###  为什么直播无法进行视频录制呢？ 
直播录制回看功能依托于腾讯云的**云点播服务**支撑，如果您想要使用录制功能，首先需要在腾讯云的管理控制台 [开通云点播服务](https://console.cloud.tencent.com/vod)。

<span id="que3"></span>
###  直播结束了要多久才能看到录制文件？ 
预计在直播完成后5分钟左右可获取录制文件，录制完成后会有事件回调，详细以收到回调时间为准，更多详情请参见 [回调配置](https://intl.cloud.tencent.com/document/product/267/31074)。

<span id="que4"></span>
### 直播录制后，如何获取录制文件？
录制文件生成后自动存储到云点播系统，需要客户开通点播服务才能存储成功。可通过以下方式获取录制文件：
- [云点播控制台](https://intl.cloud.tencent.com/document/product/267/31563)
- [录制事件通知](https://intl.cloud.tencent.com/document/product/267/31563)
- [点播 API 查询](https://intl.cloud.tencent.com/document/product/267/31563)

<span id="que5"></span>
### 直播视频能迁移吗？
目前需要您获取视频的下载地址后自己迁移。 

<span id="que6"></span>
###  如何设置视频存储时长？
云直播的视频存储目前没有时间限制，您可以通过控制台和 RSET API 接口管理视频文件。 

<span id="que7"></span>
- **录制 MP4、FLV 或 AAC 格式**：单个文件时长限制为5分钟 - 120分钟。您可以通过 [创建录制模板](https://intl.cloud.tencent.com/document/product/267/30845) 接口中的 RecordInterval 参数指定更短的分片。
	- 如果一次直播过程非常短暂，例如只有不到1秒钟时间，那么可能是没有录制文件的。
	- 如果一次直播时间不算长（小于 RecordInterval），且中途没有推流中断的事情发生，那么通常只有一个文件。
	- 如果一次直播时间很长（超过 RecordInterval ），那么会按照 RecordInterval 指定的时间长度进行分片，分片的原因是避免过长的文件在分布式系统中流转时间的不确定性。
	- 如果一次直播过程中发生推流中断（之后 SDK 会尝试重新推流），那么每次中断均会产生一个新的分片。

- **录制 HLS 格式**：最长单个文件时长无限制，如果超出续录超时时间则新建文件继续录制。续录超时时长可设置为0s - 1800s。。

<span id="que9"></span>
### 如何把碎片拼接起来？
目前腾讯云支持使用云端 API 接口拼接视频分片 。 

<span id="que10"></span>
###  只设置了一个录制模板，但是直播录制出现了两路，如何排查？ 
一般情况下，可能是当前推流域名下并发了两个录制任务。建议根据下列思路依次排查：

1. 检查控制台录制配置信息，确认录制文件类型是否选择只选择一个格式。
   - 若控制台为**新版控制台**，前往[【域名管理】](https://console.cloud.tencent.com/live/domainmanage)，单击推流域名右侧的【管理】，进入查看【模板配置】中的【录制配置】，查看关联模板“录制格式”信息。
  
2. [创建录制任务](https://intl.cloud.tencent.com/document/product/267/30847) 和 [创建录制模板](https://intl.cloud.tencent.com/document/product/267/34223) 为两种录制发起方式，实际使用中按需选择其中一种即可。若同一直播流，配置录制模板的同时创建了录制任务，会导致重复录制。请检查是否已在控制台开启录制任务同时，调用 API 3.0的  [CreateLiveRecord](https://intl.cloud.tencent.com/document/product/267/30847) 接口或 API 2.0的 Live_Tape_Start 接口发起了录制任务。

> ! 若以上方法无法解决您的问题，请 [提工单](https://console.cloud.tencent.com/workorder/category) 解决，会有专人对接。






